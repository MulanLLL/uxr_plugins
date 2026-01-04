---
name: study-planner
description: This skill should be used when the user wants to create a comprehensive UXR (User Experience Research) study plan. It uses a 3-step multi-LLM workflow combining Gemini-3's strategic narrative and vision, ChatGPT-5's critical analysis and operational refinement, and Claude's synthesis and polishing to produce high-quality research plans with learned best practices.
---

# Study Planner

This skill creates comprehensive UXR study plans using a validated 3-step multi-LLM workflow that ensures strategic depth, logical rigor, and factual accuracy.

## When to Use This Skill

Use this skill when:
- Starting a new UXR project and need a detailed study plan
- User asks to "create a study plan" or "plan a research study"
- Need to document research objectives, methodology, timeline, and deliverables
- Want to leverage best practices from previous research projects
- Require a comprehensive plan that covers all phases of UXR workflow

## The 3-Step Planning Workflow

This skill implements a Sequential Collaboration approach using three AI models, each taking on a specific UXR team role:

### Step 1: Initial Plan Generation (Principal UX Researcher: Gemini-3)
**Role:** Principal UX Researcher who crafts the comprehensive research vision, narrative and plan
**Expertise:** Research vision, strategic planning, and narrative storytelling

**Prompt Template:**
```
You are a Principal UX Researcher with 10+ years of experience leading strategic research initiatives. Draft a comprehensive and detailed study plan for [research topic/objectives].

As a Principal Researcher, focus on:
- Clear research objectives that drive business decisions
- Translating business questions and research objectives to tangible research questions
- Thoughtful methodology choices and picking the right research method (interviews, surveys, or mixed methods)
- Realistic timelines with strategic milestones
- Stakeholder communication and buy-in strategies
- Resource planning and budget justification
- Success criteria that demonstrate research impact
- Compelling narrative that connects research to business value

Include these sections:
1. Executive Summary
2. Research Objectives
3. Research Questions
4. Methodology (detailed)
5. Timeline & Milestones
6. Participant Recruitment Strategy
7. Data Collection Plan
8. Analysis Approach
9. Deliverables
10. Budget & Resources
11. Risks & Mitigation
12. Success Criteria

Apply learnings from: references/learnings.md
```

**Output:** Well-written, strategically sound initial plan with strong narrative and business alignment

### Step 2: Critical Analysis & Improvement (Research Ops Specialist: ChatGPT-5)
**Role:** Critic who refines methodology, feasibility, and logistical details
**Expertise:** Research methodology, project operations, quality assurance, resource optimization

**Prompt Template:**
```
You are a Research Operations Specialist with expertise in UXR methodology and project execution. Review the following study plan drafted by a Principal Researcher.

As a Research Ops expert, critically analyze:

1. **Methodological Rigor:**
   - Are research methods appropriate for the objectives?
   - Is sample size justified with sound reasoning?
   - Are data quality controls specified?
   - Are there gaps in the research design?

2. **Operational Feasibility:**
   - Is the timeline realistic given the scope?
   - Are resource allocations sufficient?
   - Are dependencies and bottlenecks identified?
   - Is the budget breakdown complete and justified?

3. **Process Clarity:**
   - Are all steps clearly defined and measurable?
   - Are participant recruitment logistics detailed?
   - Is data collection protocol specific enough?
   - Are analysis methods clearly specified?

4. **Risk Management:**
   - Are all major risks identified?
   - Are mitigation strategies concrete and actionable?
   - Are contingency plans realistic?

For the **Methodology section specifically**, provide:
- A technically refined alternative with precise operational details
- Specific sampling strategy and justification
- Quality assurance checkpoints throughout the process
- Step-by-step data collection and analysis procedures

[PASTE PRINCIPAL RESEARCHER'S PLAN HERE]
```

**Output:** Detailed operational critique + technically refined methodology with execution clarity

### Step 3: Final Synthesis and Validation (Lead UX Researcher: Claude)
**Role:** Synthesizer who integrates everything into a polished plan
**Expertise:** Research best practices, cross-functional collaboration, deliverable quality, industry benchmarking

**Prompt Template:**
```
You are a Lead UX Researcher with deep expertise in research excellence and industry best practices. Review the study plan and operational critique below.

As a Lead Researcher, your tasks:

A) **Integrate and Refine:**
   - Synthesize the Principal Researcher's strategic vision with the Research Ops feedback
   - Incorporate all valid operational improvements
   - Resolve any conflicting recommendations
   - Ensure the plan is both strategic AND executable
   - Maintain the compelling narrative while adding operational precision

B) **Validate Against Industry Standards:**
   Using your knowledge of UXR best practices, verify:
   - Sample size recommendations (appropriate for study type and objectives)
   - Timeline estimates (realistic for each research phase)
   - Budget benchmarks (aligned with industry standards for UXR work)
   - Methodology choices (gold standard for the research questions)
   - Deliverable formats (effective for stakeholder communication)

C) **Polish for Excellence:**
   Create the final plan with:
   - Clear, professional section structure
   - Specific, measurable details throughout
   - Evidence of methodological rigor
   - Validated factual accuracy
   - Stakeholder-ready presentation quality

Original Plan (Principal Researcher):
[PASTE GEMINI'S PLAN]

Operational Critique (Research Ops):
[PASTE CHATGPT'S CRITIQUE]
```

**Output:** Publication-ready study plan that balances strategic vision with operational excellence

## Workflow Execution

When creating a study plan, follow these steps:

### Before Starting: Gather Context
Ask the user for:
1. **Project name** - What is this research project called?
2. **Research topic** - What are you researching?
3. **Research objectives** - What business goals drive this research?
4. **Target audience** - Who are you researching?
5. **Methodology preference** - Interviews, surveys, or both?
6. **Timeline constraints** - Any deadlines or time constraints?
7. **Budget constraints** - Any budget limitations?
8. **Special requirements** - Any specific requirements or constraints?

### Step-by-Step Execution

**Step 1: Principal Researcher Draft (Gemini-3)**
1. Read `references/learnings.md` for accumulated best practices
2. Construct the Principal Researcher prompt using the template above
3. Use Gemini-3 (gemini-3-pro-preview via mcp__zen__chat)
4. Generate strategic, comprehensive plan with strong business narrative
5. Save draft as markdown directly to Google Drive Planning folder
   - File naming: `{project_name}_step1_principal_draft.md`
   - Use MCP Google Workspace tools to create markdown file
   - Keep original markdown format
   - **DO NOT** create local temp files

**Step 2: Research Ops Review (ChatGPT-5)**
1. Use ChatGPT-5 (gpt-5 or gpt-5-pro via mcp__zen__chat)
2. Paste Principal Researcher's plan into Research Ops critique prompt
3. Receive operational analysis with focus on:
   - Methodological rigor and feasibility
   - Process clarity and execution details
   - Resource optimization and risk management
4. Save Research Ops critique as markdown to Google Drive Planning folder
   - File naming: `{project_name}_step2_ops_review.md`
   - Use MCP Google Workspace tools to create markdown file
   - **DO NOT** create local temp files

**Step 3: Lead Researcher Synthesis (Claude)**
1. Use Claude (Sonnet 4.5 - the current model)
2. Provide both Principal Researcher's plan and Research Ops critique
3. Lead Researcher integrates feedback and validates against industry standards
4. Receive final plan that is both strategic AND operationally sound
5. Save final plan as markdown directly to Google Drive Planning folder
   - File naming: `{project_name}_study_plan.md`
   - Use MCP Google Workspace tools to create markdown file
   - Keep original markdown format - do NOT convert to Google Doc

**Creating Files in Google Drive (Using MCP):**

Use the MCP Google Workspace tool `mcp__google-workspace__create_drive_file` to create markdown files directly in Google Drive **without creating local temp files**:

```python
# Example: Create step 1 draft directly in Google Drive
mcp__google-workspace__create_drive_file(
    user_google_email="YOUR_EMAIL@gmail.com",
    file_name="{project_name}_step1_principal_draft.md",
    folder_id="{planning_folder_id}",  # Get this from project folder structure
    content="{generated_plan_content}",  # The markdown content
    mime_type="text/markdown"
)
```

**Important:**
- **DO NOT** create local temp files or temp folders
- Create markdown files **directly** in Google Drive using MCP tools
- All step files (step1, step2, step3) should go to the Planning/ folder in Google Drive
- Keep all step files permanently for reference

### Step 4: Human Review & Revision Loop
1. Share Google Doc link with user
2. User reviews and provides feedback via comments in Google Doc
3. **GEMINI-3 reads comments and makes revisions:**
   - Use MCP to read all Google Doc comments
   - Identify specific requested changes
   - Make revisions directly in the Google Doc
   - Mark comments as resolved as changes are made
4. **User reviews revised version:**
   - If approved → proceed to Step 5 (Learning Extraction)
   - If additional feedback → repeat Step 4
5. **Maximum 2-3 revision cycles** (ask user if more cycles needed)

### Step 5: Learning Extraction & Update (Automatic via feedback-learner)

**The feedback-learner skill automatically activates when you finish reviewing the plan.**

**How It Works:**
1. **User reviews** the study plan in Google Docs
2. **User adds comments** with specific feedback:
   - Comments with **"LEARN"** keyword (case-sensitive, all caps) → Become stored learnings
   - Regular comments (without "LEARN") → Project-specific feedback only
3. **User says**: "I've added comments" or "I've finished adding comments"
4. **feedback-learner auto-activates** and:
   - Filters for LEARN keyword only
   - Extracts context (commented text + section + surrounding paragraphs)
   - Generalizes learnings via LLM (UX principal researcher perspective)
   - Shows extracted learnings for confirmation
   - Saves to `study-planner/references/learnings.md`
   - Resolves LEARN comments (regular comments remain for your review)
5. **Next study plan** automatically applies these learnings

**Example LEARN Comments:**
- ✅ "LEARN: Include weekly timeline breakdown" → Becomes a stored learning
- ✅ "LEARN: Add link to detailed interview guide doc" → Becomes a stored learning
- ❌ "This timeline looks good" → Project-specific only, not stored
- ❌ "learn: add more detail" → Won't trigger (lowercase)

**Why LEARN Keyword?**
This prevents overgeneralization by giving you explicit control over which feedback becomes learned knowledge versus project-specific comments.

**For complete feedback-learner documentation**, see: `.claude/skills/feedback-learner/SKILL.md`

## Integration with UXR Workflow

This skill is the first major step in the UXR workflow:

**Before study-planner:**
- Desk research (optional but recommended)

**During study-planner:**
1. Generate initial plan (3-step multi-LLM workflow)
2. User review → Revision loop (repeat until approved)
3. Extract learnings → Update learnings.md

**After study-planner (plan approved):**
1. interview-guide-writer creates interview guide (if methodology includes interviews)
2. survey-creator creates survey (if methodology includes surveys)
3. Proceed to execution phase (recruitment, data collection)
4. Analysis and reporting phases follow

## Output Format

The final study plan is created as a Google Doc with this structure:

```
[Project Name] - UXR Study Plan

Executive Summary
- 2-3 paragraph overview
- Key objectives and expected outcomes

1. Research Objectives
   - Primary objective
   - Secondary objectives (2-3)
   - Success criteria for each

2. Research Questions
   - 3-5 core research questions
   - Sub-questions under each

3. Methodology
   - Research approach (qualitative/quantitative/mixed)
   - Specific methods (interviews, surveys, etc.)
   - Sample size with justification
   - Sampling strategy
   - Data quality measures

4. Timeline & Milestones
   - Week-by-week breakdown
   - Key milestones with dates
   - Dependencies

5. Participant Recruitment
   - Criteria (inclusion/exclusion)
   - Recruitment channels
   - Screening process
   - Incentive structure

6. Data Collection Plan
   - Interview protocol (if applicable)
   - Survey design (if applicable)
   - Recording and documentation approach
   - Privacy and consent procedures

7. Analysis Approach
   - Qualitative analysis methods
   - Quantitative analysis methods
   - Synthesis approach
   - Validation strategy

8. Deliverables
   - Specific outputs with formats
   - Delivery dates
   - Stakeholder presentation plan

9. Budget & Resources
   - Personnel requirements
   - Tools and software
   - Participant incentives
   - Estimated costs by category

10. Risks & Mitigation
    - Potential risks with likelihood/impact
    - Mitigation strategies
    - Contingency plans

11. Success Criteria
    - Measurable outcomes
    - Quality indicators
    - Stakeholder satisfaction measures

Appendix
- References to desk research
- Templates and tools to be used
```

## Learnings Storage

The skill maintains accumulated best practices in `references/learnings.md`:

**Learning Categories:**
- Executive Summary style and content
- Research Objectives formatting
- Timeline structure and detail level
- Methodology specificity
- Budget presentation
- Risk identification depth
- Success criteria measurability

**Learning Sources:**
- User feedback via Google Doc comments
- Post-project retrospectives
- Explicit user corrections

## Best Practices (Built-in)

The skill starts with these foundational best practices:

### Research Objectives
- ✅ Align with business goals explicitly
- ✅ Include 1 primary + 2-3 secondary objectives
- ✅ Make each objective specific and measurable
- ✅ Define success criteria for each objective

### Timeline
- ✅ Include week-by-week breakdown
- ✅ Specify start and end dates for each phase
- ✅ Build in buffer time (10-20%)
- ✅ Highlight critical path and dependencies

### Methodology
- ✅ Specify exact numbers (e.g., "12 interviews" not "user interviews")
- ✅ Include duration and format (e.g., "45-minute semi-structured interviews")
- ✅ Justify sample size with reasoning
- ✅ Detail data quality assurance measures

### Budget
- ✅ Break down by category (labor, tools, incentives, etc.)
- ✅ Include specific dollar amounts or ranges
- ✅ Compare to industry benchmarks
- ✅ Note any budget constraints and implications

### Risks
- ✅ Identify 5-7 specific risks
- ✅ Rate each by likelihood and impact
- ✅ Provide concrete mitigation strategies
- ✅ Include contingency plans for high-impact risks

## Multi-LLM Access Methods

The skill uses mcp__zen__chat to access all three models:

### Recommended: MCP Zen Integration (Current)
- Use `mcp__zen__chat` with model parameter:
  - Gemini-3: `model="gemini-3-pro-preview"` or `model="pro"`
  - ChatGPT-5: `model="gpt-5-pro"` or `model="gpt5-pro"`
  - Claude: Current session (Sonnet 4.5)
- Automated workflow without manual copying
- All models accessible via unified interface

### Fallback Options
If MCP Zen is unavailable:
- Use direct API access (OpenAI API, Google AI Studio API)
- Use web interfaces (ChatGPT, Gemini, Claude.ai)
- Manually copy/paste prompts and responses

## Error Handling

**If Gemini-3 (Principal Researcher) is unavailable:**
- Fall back to Gemini-2.5 (gemini-2.5-pro)
- If Gemini-2.5 is also unavailable, use ChatGPT-5 (gpt-5-pro)
- Note in plan: "Generated by [model name] Principal Researcher"
- Use enhanced prompting to focus on strategic vision and narrative

**If ChatGPT-5 (Research Ops) is unavailable:**
- Use Gemini-3 for research ops critique instead
- Note in plan: "Operational review by Claude Research Ops"
- Emphasize methodological rigor in critique

**If Claude (Lead Researcher) is unavailable:**
- Use ChatGPT-5 for final synthesis instead
- Note in plan: "Finalized by ChatGPT-5 Lead Researcher"
- Emphasize operational precision in final output

**If all models unavailable:**
- Use whichever model is available with enhanced prompting
- Incorporate strategic, operational, and synthesis perspectives in single prompt
- Note in plan: "Single-model plan - recommend peer review before execution"

## Usage Example

```
User: "Create a study plan for researching startup founders' needs for UX insights"

Claude (this skill):
1. Asks context questions:
   - Project name? "Startup Insights"
   - Research objectives? [user provides]
   - Target audience? "Startup founders"
   - Methodology? "Intercept interviews"
   - Timeline? "Conduct interviews at TechCrunch Disrupt, analyze within 2 days"
   - Budget? "Minimal - bootstrapped approach"

2. Executes 3-step UXR team workflow:
   - Step 1 (Gemini-3 Principal Researcher): Generates strategic, comprehensive plan with strong business narrative
   - Step 2 (ChatGPT-5 Research Ops): Reviews for methodological rigor and operational feasibility
   - Step 3 (Claude Lead Researcher): Synthesizes feedback and validates against industry standards

3. Creates Google Doc with final plan combining:
   - Strategic vision (from Gemini-3 Principal Researcher)
   - Operational precision (from ChatGPT-5 Research Ops)
   - Industry-validated best practices (from Claude Lead Researcher)

4. Moves to Planning folder

5. Shares link with user for review

User: Reviews plan, adds comments in Google Doc:
   - Comment on Timeline section: "LEARN: Include weekly timeline breakdown with owners"
   - Comment on Methodology: "LEARN: Add link to detailed interview guide doc"
   - Comment on Budget: "This looks reasonable for a bootstrap study" (no LEARN keyword)

Claude: "I see you've added 3 comments. Let me make revisions based on your feedback."

6. Makes revisions:
   - Reads all Google Doc comments via MCP
   - Updates Timeline section with weekly breakdown and owners
   - Adds link to interview guide document in Methodology section
   - Notes the budget feedback (no changes needed)
   - Marks revised comments as resolved

7. Shares updated doc: "I've revised the plan based on your feedback. Please review."

User: Reviews revisions, says: "Looks good! I've finished adding comments."

Claude (feedback-learner auto-activates): "I see you've added comments. Let me extract learnings..."

8. Extracts learnings from LEARN comments:
   - Found 2 LEARN comments (out of 3 total)
   - Extracted context for each learning
   - Generalized via LLM (UX principal researcher perspective)
   - Shows user the extracted learnings for confirmation

User: "yes" (confirms saving learnings)

Claude: "✅ Saved 2 learnings to study-planner/references/learnings.md!
        ✅ Resolved 2 LEARN comments.

        Future study plans will automatically include:
        - Weekly timelines with owner assignments and checkpoints
        - Links to detailed interview guide documents with version metadata

        Regular comment (without LEARN) remains unresolved for your review.

        Ready to proceed with creating the interview guide?"
```

## Revision Process Details

### Reading Google Doc Comments
Use MCP tool: `mcp__google-workspace__read_document_comments`
- Input: document_id, user_google_email
- Output: All comments with their locations and content
- Parse comments to identify: section, specific issue, requested change

### Making Revisions
Use MCP tool: `mcp__google-workspace__modify_doc_text` or Edit operations
- Address each comment systematically
- Make changes in the Google Doc directly
- Preserve document structure and formatting
- Add clarifying details where needed

### Resolving Comments
Use MCP tool: `mcp__google-workspace__resolve_document_comment`
- Input: document_id, comment_id, user_google_email
- Mark as resolved after addressing each comment
- Leaves audit trail of what was changed

### Revision Best Practices
1. **Read all comments first** before making any changes
2. **Group related comments** (e.g., all timeline feedback together)
3. **Make comprehensive edits** (don't just address literal comment, improve whole section)
4. **Resolve comments incrementally** as changes are made
5. **Summarize changes** for user ("I've updated 3 sections based on your 5 comments")
6. **Ask clarifying questions** if comments are ambiguous

### Handling Conflicting Feedback
If user comments contradict each other or the original plan:
- Identify the conflict explicitly
- Ask user for clarification: "I see conflicting guidance on X. Would you prefer A or B?"
- Don't guess - always confirm with user

## Technical Notes

- Plan generation takes 5-10 minutes for full 3-step workflow
- Revision cycles add 5-10 minutes each (depends on complexity)
- Google Doc creation uses MCP Google Workspace integration
- Comment reading and resolution uses MCP Google Workspace tools
- File moving uses drive-file-mover skill
- **Learning extraction uses feedback-learner skill** (auto-triggers on "I've added comments")
  - Only processes comments with "LEARN" keyword (case-sensitive)
  - Extracts context and generalizes via LLM
  - Saves to `references/learnings.md`
  - Auto-resolves LEARN comments after saving
- All learnings persist across projects and sessions
- Next study plan automatically reads and applies all learnings

## Future Enhancements

Potential improvements:
- Automated API integration for GPT and Gemini
- Template variations for different research types (generative, evaluative, etc.)
- Integration with project management tools
- Automated timeline visualization
- Budget comparison with historical data
