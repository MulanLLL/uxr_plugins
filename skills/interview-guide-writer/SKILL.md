---
name: interview-guide-writer
description: This skill should be used when creating comprehensive interview guides for UXR studies. Automatically activated when the user asks to create interview guides based on a study plan or requests standalone interview guide documents. Generates detailed scripts including opening/closing, consent language, core questions with probes, timing guidance, and field note templates.
---

# Interview Guide Writer

## Overview

The interview-guide-writer skill transforms UXR study plans into comprehensive, ready-to-use interview guides. When research plans specify interviews as a methodology, this skill creates detailed interviewer scripts with opening/closing language, consent protocols, structured questions with probes, timing guidance, and post-interview documentation templates.

## When to Use This Skill

**Automatic activation**:
- User says "create interview guide" or "write interview guide"
- User references a study plan and requests interview materials
- User asks to "extract interview questions from the study plan"

**Manual activation**:
- User provides a study plan document and asks for interview guides
- User wants to formalize research questions into interviewer scripts

**Trigger phrases**:
- "create interview guides based on the study plan"
- "write detailed interview scripts"
- "generate interviewer materials"
- "create interview guide for [study name]"

## Workflow: Creating Interview Guides

### Step 1: Read the Study Plan

Read the complete study plan document to extract:
- **Research objectives**: What the study aims to accomplish
- **Research questions**: Core and sub-questions already defined
- **Interview methodology**: Number of interviews, duration, structure (structured/semi-structured/unstructured)
- **Sample composition**: Who will be interviewed (roles, stages, characteristics)
- **Interview approach**: Any special considerations (intercept, remote, in-person)
- **Multiple interview guides**: Some studies use alternating guides (Guide A, Guide B) to cover different question sets while maintaining depth

### Step 2: Structure the Interview Guide Document

Create a comprehensive interview guide document with these sections:

**1. Document Header**
- Project name and study title
- Interview type and duration
- Date and version

**2. Overview Section**
- Brief description of the study
- Interview methodology summary
- If multiple guides: explain the alternating strategy and when to use each

**3. Pre-Interview: Approach & Screening**
- Initial approach script (how to introduce the study)
- Screening questions to qualify participants
- Transition script to begin the interview

**4. Opening Script (Consent & Introduction)**
- Recording consent language
- Privacy and anonymization assurances
- Purpose of research explanation
- Time expectation setting
- Explicit consent capture

**5. Core Questions**
For each core question:
- **Opening question**: The main question to ask
- **Follow-up probes**: 2-4 sub-questions to go deeper
- **Timing guidance**: How long to spend on this question
- **Transition**: How to move to the next question
- **Listening notes**: What to listen for in responses

**6. Closing Script**
- Wrap-up and thanks
- Recap of what happens next
- Opportunity for participant questions
- Final thanks and next steps

**7. Post-Interview: Field Notes Template**
- Participant profile fields
- Key observations capture
- Quality check items (audio, depth, issues)

**8. Appendix**
- Interviewer tips and best practices
- Handling common challenges
- Consent and ethics reminders
- Recording best practices
- Participant tracking sheet template

### Step 3: Extract and Expand Research Questions

Transform research questions from the study plan into interview-ready scripts:

**From study plan** → **To interview guide**:
- Core research question → Opening question + 3-4 follow-up probes
- Sub-questions → Specific probes with natural conversation flow
- Research objectives → Questions that elicit the needed insights

**Key principles**:
- Use open-ended questions (avoid yes/no)
- Frame questions in natural, conversational language
- Add probes that dig deeper ("Can you say more about that?", "Walk me through a specific example")
- Include timing guidance for each question block
- Add transition phrases between sections

### Step 4: Add Interview Best Practices

Include practical guidance for interviewers:

**Opening techniques**:
- How to build rapport quickly
- Consent language that feels natural
- Setting time expectations clearly

**Probing strategies**:
- Use silence (2-3 second pause after they finish)
- Reflect back ("You mentioned X was frustrating—can you say more?")
- Ask for examples ("Walk me through a specific time when...")
- Follow the energy (dig deeper where they light up)

**Time management**:
- Keep an eye on the clock
- Prioritize depth over breadth
- Be comfortable cutting off tangents politely

**Handling challenges**:
- Rushed or distracted participants
- Surface-level answers (probe for specifics)
- Off-topic rambling (gently redirect)
- Defensive or guarded responses (reassure anonymity)
- Noisy environments (move or hold recorder close)

### Step 5: Create Supporting Materials

Generate templates and tracking tools:

**Participant Tracking Sheet**:
- Table to monitor sample diversity in real-time
- Columns: Participant #, Guide Used, Role, Stage, Product Type, Industry, Recording File, Notes
- Include abbreviation key for quick note-taking

**Field Notes Template**:
- Participant profile (role, stage, product type, industry)
- Recording file name
- Key observations (1-2 sentences)
- Quality check (audio quality, depth of responses, technical issues)

### Step 6: Format for Readability

Structure the document for easy use during interviews:

**Clear hierarchy**:
- Use heading levels consistently (H1 for major sections, H2 for subsections)
- Bold key instructions and questions
- Use italics for probes and follow-ups

**Visual separation**:
- Use horizontal rules (---) to separate major sections
- Box or highlight critical consent language
- Use tables for tracking sheets

**Timing indicators**:
- Include time estimates for each section
- Example: "### Core Question 1 (2.5 minutes)"

## Multiple Interview Guides Strategy

When a study plan specifies multiple interview guides (e.g., Guide A and Guide B):

**Purpose**: Cover more ground while maintaining depth per interview
- Guide A focuses on one set of core questions
- Guide B focuses on a different set of core questions
- Alternating between guides ensures comprehensive coverage across the sample

**Implementation**:
- Create distinct sections for each guide in the document
- Explain the alternating strategy clearly in the Overview
- Suggest: "Use Guide A with odd-numbered participants (1, 3, 5...) and Guide B with even-numbered participants (2, 4, 6...)"
- Ensure both guides have the same opening/closing scripts and duration
- Both guides should share the same approach, screening, and consent language

**Tracking**:
- Participant tracking sheet includes "Guide Used" column
- Ensures balanced use of both guides across the sample

## Output Format

Create a Google Doc or Markdown file with the complete interview guide content. The document should be:

**Comprehensive**: Include everything an interviewer needs (no external references required)
**Ready-to-use**: Interviewer can print and use immediately
**Well-organized**: Clear sections, good visual hierarchy, easy to navigate during an interview
**Practical**: Focus on actionable guidance, not theoretical concepts

## Integration with UXR Workflow

**Phase 2: Execution (Research Design)**
1. Study plan created and approved (Phase 1 complete)
2. **Interview guide creation** ← This skill activates here
3. Human review and approval of interview guides
4. Survey creation (if applicable)
5. Proceed to recruitment and fielding

**Inputs**: Approved study plan document
**Outputs**:
- Comprehensive interview guide document (Google Doc or Markdown)
- Ready for stakeholder review and approval
- Ready for interviewer use in the field

## Reference Materials

This skill includes reference documentation in `references/`:

### interview_best_practices.md
Comprehensive guide to qualitative interviewing techniques:
- Building rapport and trust
- Question types and when to use them
- Probing techniques and follow-up strategies
- Active listening and note-taking
- Common pitfalls and how to avoid them
- Handling difficult situations
- Consent and ethics guidelines

**When to use**: Load this file when creating interview guides to ensure best practices are incorporated. Particularly useful for:
- Crafting effective probe questions
- Structuring question flow
- Adding interviewer tips and handling guidance

## Assets

This skill includes template assets in `assets/`:

### participant_tracking_template.md
Ready-to-use table template for monitoring sample diversity during fielding

### field_notes_template.md
Structured template for post-interview documentation

**When to use**: Copy these templates directly into the interview guide document as appendices.

## Example Usage

**User request**: "Create interview guides based on the study plan @startups_insights_step3_final.md"

**Skill workflow**:
1. Read the study plan document
2. Extract: 2 interview guides (A and B), 10-minute duration, 3 core questions each
3. Generate comprehensive interview guide document with:
   - Overview explaining the 2-guide alternating strategy
   - Pre-interview approach and screening scripts
   - Opening consent script
   - Interview Guide A: 3 core questions with probes and timing
   - Interview Guide B: 3 core questions with probes and timing
   - Closing script
   - Field notes template
   - Participant tracking sheet
   - Interviewer tips appendix
4. Create Google Doc in the project's Interviews/ folder
5. Present to user for review

## Success Criteria

The interview guide is effective when:

1. ✅ Interviewer can conduct the entire interview using only this guide
2. ✅ All consent and ethics language is included and clear
3. ✅ Questions naturally elicit the insights needed for research objectives
4. ✅ Timing guidance helps interviewer stay on track
5. ✅ Probes and follow-ups enable depth beyond surface responses
6. ✅ Practical tips help interviewer handle common challenges
7. ✅ Post-interview documentation is streamlined and complete

---

*This skill works seamlessly with study-planner (Phase 1) and prepares materials for fielding (Phase 3).*
