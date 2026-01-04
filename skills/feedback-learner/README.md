# feedback-learner

> Automatically extracts learnings from Google Doc comments marked with LEARN keyword

## Overview

The feedback-learner skill is the core learning engine of the UXR Workflow Skills system. It automatically extracts generalizable patterns from your feedback and stores them as learnings that all skills apply in future projects.

**Key Innovation**: Only comments containing "LEARN" (all caps) become stored learnings. This prevents over-generalization and gives you explicit control over what becomes permanent knowledge.

## When to Use

**Auto-Activation Triggers**:
- "I've added comments"
- "I've finished adding comments"
- "Ready to extract learnings"
- "Process my feedback"

**The skill activates automatically when you finish reviewing skill outputs.**

## Features

### Core Capabilities

- **LEARN Keyword System**: Case-sensitive filtering for explicit learning control
- **Context Extraction**: Captures quoted text, section, and surrounding paragraphs
- **LLM Generalization**: Uses Gemini-3 as UX principal researcher to generalize patterns
- **Automatic Skill Identification**: Maps learnings to source skill based on folder location
- **Learning Confirmation**: Shows extracted learnings before saving
- **Auto-Resolution**: Resolves LEARN comments after extraction
- **Markdown Storage**: Human-readable learnings.md files (no database needed)

### 8-Step Workflow

1. **Get Document Info**: Identifies the document you reviewed
2. **Read All Comments**: Fetches all comments from Google Doc
3. **Filter for LEARN**: Case-sensitive word boundary matching for "LEARN"
4. **Extract Context**: Captures quoted text, section headers, surrounding paragraphs
5. **Generalize via LLM**: Gemini-3 converts specific feedback to generalizable pattern
6. **Identify Source Skill**: Maps to skill based on Google Drive folder location
7. **Show for Confirmation**: Displays extracted learnings for your review
8. **Save & Resolve**: Appends to learnings.md and resolves LEARN comments

## Installation

The skill is automatically installed when you install the uxr-workflow-skills plugin:

```bash
# Install via plugin commands
/plugin marketplace add MulanLLL/uxr_plugins
/plugin install uxr-workflow-skills@MulanLLL
```

Manual installation (alternative):

```bash
# Clone repository
git clone https://github.com/MulanLLL/uxr_plugins.git

# Copy skill to Claude Code skills directory
cp -r uxr_plugins/skills/feedback-learner ~/.claude/skills/
```

## Dependencies

### Required

- **Claude Code**: Main platform (claude.ai/code)
- **Google Workspace Account**: For reading Doc comments
- **Google Workspace MCP Server**: For Docs and Drive operations
- **Zen MCP Server**: For LLM generalization via Gemini-3

See [docs/MCP_SETUP.md](../../docs/MCP_SETUP.md) for configuration instructions.

## Usage

### Basic Workflow

1. **Review Skill Output**:
   - Open Google Doc created by any skill (study-planner, interview-guide-writer, etc.)
   - Read through the content

2. **Add Comments**:
   - **LEARN comments**: For patterns to remember
     - ✅ "LEARN: Add weekly breakdown"
     - ✅ "LEARN this for future"
     - ✅ "Please LEARN to include..."
   - **Regular comments**: For project-specific feedback
     - ✅ "Change this to Q2 instead of Q1"
     - ✅ "Add stakeholder names here"

3. **Trigger Extraction**:
   ```
   User: "I've added comments"
   ```

4. **Review Extracted Learnings**:
   - Claude shows generalized learnings
   - Confirm they're correct and useful
   - Learnings are saved to skill's learnings.md

5. **Future Projects**:
   - Learnings automatically applied
   - No manual reminder needed

### Example Conversation

```
User: "I've added comments in the study plan doc"

Claude: I'll extract learnings from your comments...

[Reads document]
[Filters for LEARN keyword]
[Extracts context]
[Generalizes via Gemini-3]

I found 3 LEARN comments. Here are the extracted learnings:

**From: Timeline Section**
- Original comment: "LEARN: Too vague"
- On text: "Timeline: 4 weeks"
- Learning: "Include weekly timeline with specific milestones and deliverables for each week"

**From: Methodology Section**  
- Original comment: "LEARN this for next time"
- On text: "Conduct user interviews"
- Learning: "Specify exact numbers (e.g., '12 interviews') instead of vague terms, and include duration and format (e.g., '45-minute semi-structured interviews')"

**From: Deliverables Section**
- Original comment: "LEARN: Add this to all future plans"
- On text: "Final report"
- Learning: "Specify deliverable formats (slide deck vs written report vs both) and include page/slide counts"

I'll save these to study-planner/references/learnings.md and resolve the LEARN comments.

Would you like me to proceed?

User: "Yes, save them"

Claude: ✅ Learnings saved to study-planner/references/learnings.md
✅ LEARN comments resolved
✅ Regular comments (2) left for you to address

Next time study-planner runs, these patterns will be automatically applied!
```

## LEARN Keyword Filtering

### Valid LEARN Comments

The keyword must be **all caps** and a **complete word**:

✅ Valid:
- "LEARN this for future studies"
- "LEARN: Include weekly breakdown"
- "Please LEARN to add this section"
- "We should LEARN from this"

❌ Not Valid (will be ignored):
- "learn this" (lowercase)
- "LEARNING from this" (different word)
- "LEARNED this pattern" (different word)
- "We should remember this" (no LEARN keyword)

### Why Case-Sensitive?

Prevents accidental extraction of general comments:
- "I learned something interesting here" (not a learning directive)
- "This is a learning opportunity" (not a learning directive)

Only intentional, explicit LEARN keywords trigger extraction.

## Configuration

### Customizing Generalization Prompt

The skill uses Gemini-3 with a UX research principal researcher persona. You can customize this in SKILL.md:

```markdown
Take the persona of a senior UX research principal with 15+ years experience.
Generalize this feedback into an actionable guideline for future research plans.
```

Modify to match your organization's voice or domain.

### Learning Storage Format

Learnings are stored in markdown format:

```markdown
# Learnings - Skill Name

## Section Name
- Learning pattern (learned from: Project X, 2026-01-03)
- Another pattern (learned from: Project Y, 2026-01-15)

## Another Section  
- Different pattern (learned from: Project Z, 2026-02-01)
```

This format:
- Is human-readable
- Tracks context (project, date)
- Organizes by document section
- Version controls with git

## Examples

### Example 1: Study Plan Learning

**First Project**:
```
Comment: "LEARN: Timeline too vague"
On text: "Timeline: 4 weeks"
Section: Timeline
```

**Extracted Learning**:
```markdown
## Timeline Section
- Include weekly timeline with specific milestones (learned from: Mobile App Study, 2026-01-15)
```

**Second Project**:
Study plan automatically includes:
```
Timeline:
Week 1: Desk research and literature review
Week 2: Survey design and pilot testing
Week 3: Survey distribution and recruitment
Week 4: Analysis and reporting
```

### Example 2: Interview Guide Learning

**First Project**:
```
Comment: "LEARN this: Need warm-up before sensitive questions"
On text: "Question 1: Tell me about your financial struggles"
Section: Core Questions
```

**Extracted Learning**:
```markdown
## Core Questions Section
- Include 1-2 warm-up questions before sensitive topics (learned from: Finance Study, 2026-01-20)
```

**Second Project**:
Interview guide automatically includes warm-up:
```
Background Questions (5 min):
1. Tell me about your current role and responsibilities
2. How long have you been in this position?

Financial Questions (15 min):
3. Now let's talk about budgeting...
```

### Example 3: Multiple Skills Learning

feedback-learner can extract learnings for any skill:

```
study-planner/references/learnings.md
interview-guide-writer/references/learnings.md
survey-creator/references/learnings.md
report-generator/references/learnings.md
```

Each skill reads its own learnings.md automatically.

## Troubleshooting

### Common Issues

**Issue**: "No LEARN comments found"
- **Solution**: Verify comments use "LEARN" in all caps
- **Check**: Word boundary matching (not "LEARNED" or "LEARNING")

**Issue**: "Cannot read document comments"
- **Solution**: Ensure Google Workspace MCP is authenticated
- **Check**: Try reading comments manually via MCP

**Issue**: "Zen MCP not available for generalization"
- **Solution**: Install Zen MCP with Gemini-3 access
- **Alternative**: Skill can use Claude for generalization (fallback)

**Issue**: "Learning saved to wrong skill"
- **Solution**: Verify document is in correct Google Drive folder
- **Mapping**: Planning/ → study-planner, Interviews/ → interview-guide-writer

**Issue**: "Learning too specific / not generalizable"
- **Solution**: Provide clearer LEARN comment with context
- **Example**: Instead of "LEARN: Fix this", use "LEARN: Include specific metrics in this section"

**Issue**: "Regular comments were resolved (shouldn't be)"
- **Solution**: Verify those comments contained "LEARN" keyword
- **Check**: Case-sensitive exact match required

### Getting Help

- **Documentation**: [docs/LEARNING_SYSTEM.md](../../docs/LEARNING_SYSTEM.md)
- **Issues**: [GitHub Issues](https://github.com/MulanLLL/uxr_plugins/issues)
- **Discussions**: [GitHub Discussions](https://github.com/MulanLLL/uxr_plugins/discussions)

## Technical Details

### File Structure

```
feedback-learner/
├── SKILL.md                    # 384 lines - Skill definition with 8-step workflow
├── README.md                   # This file
└── references/
    └── learnings_template.md   # Learning format examples
```

### Workflow Architecture

```
User: "I've added comments"
    ↓
Get Document Info (URL or search)
    ↓
Read All Comments from Google Doc
    ↓
Filter: LEARN Keyword (case-sensitive)
    ↓
Extract Context (quoted text, section, paragraphs)
    ↓
Generalize via Gemini-3 (UX principal researcher)
    ↓
Identify Source Skill (folder-based mapping)
    ↓
Show Learnings for Confirmation
    ↓
User Confirms → Save & Resolve
    ↓
Append to skill's learnings.md
Resolve LEARN comments
```

### Folder-to-Skill Mapping

The skill identifies source skill based on Google Drive folder:

```
Planning/ → study-planner
Surveys/ → survey-creator
Interviews/ → interview-guide-writer
Analysis/ → data-analyzer
Reports/ → report-generator
```

This ensures learnings are saved to the correct skill's learnings.md.

### Generalization Prompt

The LLM receives:
- Original comment text
- Quoted text from document
- Document section header
- Surrounding paragraphs (context)
- Persona: Senior UX research principal

Output:
- Actionable guideline
- Generalizable pattern
- Specific enough to be useful

## Why This Approach Works

### Explicit Control

LEARN keyword gives you control:
- ✅ "This is important to remember" → Add LEARN
- ✅ "This is project-specific" → Regular comment

No guessing what becomes permanent knowledge.

### Context-Aware

Captures full context:
- What was said (comment)
- What it refers to (quoted text)
- Where it appears (section)
- Why it matters (surrounding content)

Prevents misunderstanding feedback intent.

### Generalizable

LLM converts:
- "Change Q2 to Q3" → Doesn't become a learning (project-specific)
- "LEARN: Include quarter breakdown" → "Specify quarters for timeline sections"

Ensures learnings apply to future projects.

### No Database

Markdown files are:
- Human-readable (just open the file)
- Version controlled (git history)
- Easy to share (commit and push)
- Transparent (see exactly what was learned)

No complex infrastructure needed.

## Version History

- **v1.0.0** (2026-01-03): Initial release with LEARN keyword system and 8-step workflow

## Contributing

We welcome contributions! Ways to help:

- **Report filtering edge cases**: Help identify LEARN keyword edge cases
- **Improve generalization**: Suggest better prompt engineering
- **Enhance documentation**: Clarify the learning system
- **Share examples**: Demonstrate successful learning extraction

See [CONTRIBUTING.md](../../CONTRIBUTING.md) for guidelines.

## License

Apache License 2.0 - See [LICENSE](../../LICENSE) for details.

---

**Part of the UXR Workflow Skills plugin** | [Main Documentation](../../README.md) | [Learning System Documentation](../../docs/LEARNING_SYSTEM.md)
