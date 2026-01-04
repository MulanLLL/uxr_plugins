# feedback-learner

**Type**: Automated Learning Extraction
**Status**: Active
**Auto-Trigger**: Yes (activates on "I've added comments", "I've finished adding comments", etc.)

## Purpose

Automatically extracts generalizable learnings from Google Doc comments marked with the "LEARN" keyword (case-sensitive) and updates the appropriate skill's learnings.md file. This prevents overgeneralization by giving users explicit control over which feedback becomes learned knowledge versus project-specific comments.

## When This Skill Activates

**Auto-Trigger Phrases**:
- "I've added comments"
- "I've finished adding comments"
- "Review my feedback"
- "Extract learnings from the doc"
- "Done with comments"

The skill automatically activates when the user indicates they've finished reviewing and adding comments to a document.

## Core Workflow

### Step 1: Get Document Information
1. Ask user for document link or ID
2. Verify document is accessible via Google Workspace MCP

### Step 2: Read All Comments
Use `mcp__google-workspace__read_document_comments`:
```python
comments = mcp__google-workspace__read_document_comments(
    document_id=document_id,
    user_google_email="YOUR_EMAIL@gmail.com"
)
```

### Step 3: Filter for LEARN Keyword
Apply case-sensitive word boundary matching:
```python
import re

def has_learn_keyword(comment_text: str) -> bool:
    """
    Check if comment contains LEARN keyword (case-sensitive)
    Uses word boundary to match LEARN but not LEARNING, LEARNED, etc.
    """
    pattern = r'\bLEARN\b'
    return bool(re.search(pattern, comment_text))

learn_comments = [c for c in comments if has_learn_keyword(c['content'])]
```

If no LEARN comments found:
- Inform user: "No LEARN comments found. Only comments with 'LEARN' (all caps) are extracted as learnings."
- Exit workflow

### Step 4: Extract Context for Each LEARN Comment

For each LEARN comment, gather:

1. **Commented Text**: From `comment.quotedFileContent`
2. **Full Document Content**:
```python
doc_content = mcp__google-workspace__get_doc_content(
    document_id=document_id,
    user_google_email="YOUR_EMAIL@gmail.com"
)
```

3. **Section Header**: Search backwards from comment position for nearest markdown header
```python
def find_section_header(doc_content: str, comment_position: int) -> str:
    """
    Search backwards from comment to find nearest markdown header

    Looks for:
    - ## Research Objectives
    - ## Timeline & Milestones
    - ## Methodology

    Returns: "Research Objectives Section", "Timeline Section", etc.
    """
    lines = doc_content.split('\n')
    comment_line = get_line_number(doc_content, comment_position)

    # Search backwards
    for i in range(comment_line, -1, -1):
        line = lines[i].strip()
        if re.match(r'^#{2,4}\s+(.+)$', line):
            header = re.match(r'^#{2,4}\s+(.+)$', line).group(1)
            return f"{header} Section"

    return "General"
```

4. **Surrounding Paragraphs**: Extract 1 paragraph before + 1 paragraph after commented text

5. **Project Name**: Extract from document title

### Step 5: Generalize Learning via LLM

For each LEARN comment, use `mcp__zen__chat` to generalize:

```python
prompt = f"""You are a UX research principal researcher. Analyze this feedback and extract a generalizable learning for future UXR studies.

## Context
**Project Name**: {project_name}
**Document Section**: {section}
**Date**: {current_date}

## Feedback
**User Comment**: {comment_text}
**Commented Text**: "{commented_text}"
**Surrounding Context**: {surrounding_context}

## Task
Infer what the user REALLY wants (not just literal comment) and create a generalizable learning that can be applied to future research projects. Focus on creating actionable knowledge that improves future study quality.

**Output Format** (match existing learnings.md style):

#### Learning Title (Learned: {Month} {Year})
Description of the generalizable learning for future studies...
- ❌ Avoid: [Anti-pattern example from commented text]
- ✅ Better: [Best practice example]
- **Why**: [Rationale for why this learning matters for future research]

Output only the formatted learning - no explanations."""

learning = mcp__zen__chat(
    prompt=prompt,
    model="gemini-3-pro-preview",  # Use Gemini-3 to extract generalizable learnings from Google Doc comments
    working_directory_absolute_path="/Users/lancheng/work/UXR_workflow"
)
```

### Step 6: Identify Source Skill

Map document's folder location to the skill that created it:

```python
SKILL_FOLDER_MAP = {
    'Planning': 'study-planner',
    'Interviews': 'interview-guide-writer',
    'Surveys': 'survey-creator',
    'Analysis': 'data-analyzer',
    'Reports': 'report-generator'
}

def identify_skill_from_document(document_id: str) -> str:
    """
    Identify which skill created a document based on folder location

    1. Get file metadata from Drive
    2. Extract parent folder ID
    3. Get parent folder name (e.g., "Planning")
    4. Map to skill (e.g., "study-planner")
    """
    file_metadata = mcp__google-workspace__get_drive_file_permissions(
        file_id=document_id,
        user_google_email="YOUR_EMAIL@gmail.com"
    )

    # Get parent folder name from metadata
    parent_folder_name = extract_folder_name(file_metadata)

    skill_name = SKILL_FOLDER_MAP.get(parent_folder_name, 'unknown')
    return skill_name
```

### Step 7: Show User Extracted Learnings

Format all extracted learnings for user review:

```
Found {n} LEARN comments. Here are the extracted learnings:

Learning 1 - {Section} Section
{formatted_learning_1}
- From comment: "{original_comment_1}"

Learning 2 - {Section} Section
{formatted_learning_2}
- From comment: "{original_comment_2}"

Should I save these to {skill_name}/references/learnings.md? (yes/no)
```

### Step 8: Save & Resolve (If User Approves)

**A. Check for Duplicates**:
```python
from difflib import SequenceMatcher

def is_duplicate_learning(new_learning: str, existing_content: str) -> bool:
    """
    Check if learning already exists using title similarity
    >80% match = duplicate
    """
    new_title = extract_learning_title(new_learning)
    existing_learnings = extract_all_learnings(existing_content)

    for existing in existing_learnings:
        existing_title = extract_learning_title(existing)
        similarity = SequenceMatcher(None, new_title, existing_title).ratio()

        if similarity > 0.8:
            return True

    return False
```

**B. Append to learnings.md**:
```python
def append_learning(skill_name: str, section: str, learning: str):
    """
    Append new learning to learnings.md

    - If section exists: append to it
    - If section doesn't exist: create new section
    - Skip duplicates
    """
    file_path = f".claude/skills/{skill_name}/references/learnings.md"

    existing_content = read_file(file_path)

    # Check for duplicates
    if is_duplicate_learning(learning, existing_content):
        print(f"Skipping duplicate learning: {extract_learning_title(learning)}")
        return

    # Find or create section
    if f"## {section}" in existing_content:
        updated = insert_into_section(existing_content, section, learning)
    else:
        updated = existing_content + f"\n\n## {section}\n\n{learning}\n"

    write_file(file_path, updated)
```

**C. Resolve LEARN Comments**:
```python
for comment_id in learn_comment_ids:
    mcp__google-workspace__resolve_document_comment(
        document_id=document_id,
        comment_id=comment_id,
        user_google_email="YOUR_EMAIL@gmail.com"
    )
```

**D. Confirm to User**:
```
Saved {n} learnings to {skill_name}/references/learnings.md!
Resolved {n} LEARN comments.

Future {skill_name} runs will automatically apply these learnings.
```

## Error Handling

**Document Not Found**:
- Verify document ID is correct
- Check user has access to document
- Provide clear error message

**No LEARN Comments**:
- Inform user about LEARN keyword requirement
- Suggest adding LEARN to comments they want captured

**Duplicate Learning**:
- Skip silently and note in final summary
- "Skipped 1 duplicate learning"

**Invalid Folder Mapping**:
- If document isn't in a known folder (Planning, Interviews, etc.)
- Ask user which skill should receive the learnings

## Integration with Other Skills

**After study-planner creates a document**:
1. User reviews in Google Docs
2. User adds LEARN comments
3. User says "I've added comments"
4. feedback-learner auto-activates
5. Learnings saved to study-planner/references/learnings.md
6. Next study-planner run reads learnings.md and applies automatically

**Same workflow for**:
- interview-guide-writer
- survey-creator
- data-analyzer
- report-generator

## Example Usage

### Full Workflow Example

**User**: "I've finished adding comments to the study plan"

**Claude (feedback-learner activates)**:
```
Which document did you add comments to? Please provide the link or document ID.
```

**User**: [provides Google Doc link]

**Claude**:
```
Reading comments from document...
Found 3 comments, filtering for LEARN keyword...
Found 2 LEARN comments. Extracting context and generalizing...

Learning 1 - Timeline Section
#### Weekly Timeline Breakdown (Learned: November 2025)
Include week-by-week timeline with specific activities and milestones, not just total duration.
- ❌ Avoid: "Timeline: 4 weeks" (vague, no milestones)
- ✅ Better: "Week 1 (Oct 27-Nov 2): Recruitment. Week 2 (Nov 3-9): Interviews (4/day)."
- **Why**: Weekly breakdown enables better tracking and shows operational rigor
- From comment: "LEARN: Too vague - needs weekly breakdown"

Learning 2 - Methodology Section
#### Interview Duration Specification (Learned: November 2025)
Always specify exact interview duration and format in methodology section.
- ❌ Avoid: "12 interviews" (missing duration/format)
- ✅ Better: "12 semi-structured interviews, 45 minutes each, conducted via Zoom"
- **Why**: Duration impacts participant recruitment, scheduling, and budget planning
- From comment: "LEARN: Specify interview duration and format"

Identified source skill: study-planner (from Planning/ folder)

Should I save these 2 learnings to study-planner/references/learnings.md? (yes/no)
```

**User**: "yes"

**Claude**:
```
✅ Saved 2 learnings to study-planner/references/learnings.md!
✅ Resolved 2 LEARN comments.

Future study plans will automatically include:
- Weekly timeline breakdowns with specific milestones
- Exact interview duration and format specifications

Regular comment (without LEARN) remains unresolved for your review.
```

## Technical Notes

**MCP Tools Used**:
- `mcp__google-workspace__read_document_comments` - Read all comments
- `mcp__google-workspace__get_doc_content` - Get full document
- `mcp__google-workspace__get_drive_file_permissions` - Get folder metadata
- `mcp__google-workspace__resolve_document_comment` - Mark comments resolved
- `mcp__zen__chat` - LLM generalization

**File Operations**:
- Read: `.claude/skills/{skill_name}/references/learnings.md`
- Write: Append new learnings to appropriate sections

**Performance**:
- ~5-10 seconds per learning (LLM generalization)
- Batch processing of multiple LEARN comments
- Efficient duplicate detection

## Success Metrics

✅ Only LEARN comments processed (case-sensitive word boundary)
✅ Auto-activation when user finishes adding comments
✅ Context captured: text + section + surrounding paragraphs
✅ Learnings generalized via UX principal researcher perspective
✅ Correct skill identified via folder mapping
✅ No duplicate learnings stored
✅ LEARN comments auto-resolved
✅ User confirms before saving
✅ Learnings auto-applied in next project

## Future Enhancements

- Support for learning priority levels (critical, high, medium, low)
- Learning analytics dashboard (most applied learnings, trends)
- Cross-skill learnings (learnings that apply to multiple skills)
- Learning expiration/deprecation (mark outdated learnings)
- Batch learning extraction from multiple documents
