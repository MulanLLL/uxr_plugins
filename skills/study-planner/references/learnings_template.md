# Learned Patterns for UXR Study Planning

This file accumulates best practices learned from user feedback across multiple UXR projects. The study-planner skill reads this file before generating each plan to apply accumulated wisdom.

---

## Executive Summary Section

### Content Guidelines
- Keep to 2-3 paragraphs maximum
- First paragraph: Project context and business need
- Second paragraph: Research approach and methodology
- Third paragraph: Expected outcomes and timeline
- Include key numbers: participant count, timeline duration, primary deliverable

### Style Guidelines
- Write for executive audience (assume 2-minute read time)
- Lead with business impact, not research details
- Use clear, jargon-free language
- Avoid methodological details (save for Methodology section)

---

## Research Objectives Section

### Formatting
- **Primary Objective**: One clear, measurable objective aligned with business goal
- **Secondary Objectives**: 2-3 supporting objectives that add depth
- **Success Criteria**: Specific, measurable criteria for each objective

### Content Guidelines
- Start each objective with action verb (Understand, Identify, Evaluate, etc.)
- Connect each objective explicitly to business goal or decision
- Make success criteria SMART (Specific, Measurable, Achievable, Relevant, Time-bound)
- Avoid vague objectives like "learn about users" - be specific about what insights are needed

### Example Format
```
Primary Objective:
Understand how startup founders prioritize UX research investments relative to other business needs.

Success Criteria:
- Identify top 3 competing priorities
- Quantify perceived value of UX research (scale 1-10)
- Understand decision-making framework for budget allocation

Secondary Objectives:
1. Identify blockers to UX research adoption beyond price
2. Evaluate current methods founders use for user feedback
```

---

## Research Questions Section

### Structure
- 3-5 core research questions maximum
- 2-4 sub-questions under each core question
- Order by priority (most critical first)

#### Time-Constrained Interview Limits (Learned: October 2025)
For brief interviews (10 minutes or less), limit to **3 core questions maximum** per interview guide.
- ❌ Avoid: 4+ core questions in a 10-minute interview guide
- ✅ Better: 3 core questions with focused sub-questions
- **Why**: 4+ questions force surface-level responses; 3 allows adequate time for depth and follow-up probes

### Content Guidelines
- Make questions open-ended (avoid yes/no)
- Focus on "why" and "how" over "what"
- Ensure questions map to research objectives
- Frame for discovery, not validation of assumptions

### Quality Checks
- ❌ Avoid: "Do you use UX research?" (yes/no)
- ✅ Better: "How do you currently gather user insights for product decisions?"
- ❌ Avoid: "Is design important?" (assumes importance)
- ✅ Better: "What role does design quality play in your product strategy?"

#### Barrier/Challenge Questions (Learned: October 2025)
When asking about barriers or challenges, include ALL major types in the question - don't exclude the most obvious one.
- ❌ Avoid: "Beyond price, what other barriers do you face?"
- ✅ Better: "What are the top barriers you face? (Examples: price, time, resources, knowledge...)"
- **Why**: Users want comprehensive assessment; "beyond X" artificially excludes a critical factor that should be assessed alongside others

#### Budget/Pricing Questions (Learned: October 2025)
Frame willingness-to-pay as direct comparison to current priorities, not vague references to unrelated past expenses.
- ❌ Avoid: "When you think about your last major expense, where would a $5,000 project fit in?"
- ✅ Better: "If you had a $5,000 budget for this, how would that compare to other investments you'd consider making right now? What else would be competing for that same budget?"
- **Why**: Direct comparisons elicit more thoughtful, grounded responses about trade-offs and real decision-making context

---

## Methodology Section

### Required Specificity
- **Exact numbers**: "12 interviews" not "user interviews"
- **Duration and format**: "45-minute semi-structured interviews" not "interviews"
- **Sample composition**: "6 pre-seed founders, 6 seed-stage founders"
- **Rationale**: Justify sample size and composition choices

### For Interviews
- Specify interview structure (structured, semi-structured, unstructured)
- Include interview duration
- Note recording approach
- Detail analysis method (thematic analysis, grounded theory, etc.)

#### Include a versioned, linked interview guide in the study plan (Learned: December 2025)
Always link to a single, versioned, detailed interview guide from the study plan so interviewers and stakeholders can access the full script, probes, consent text, timing notes, and contingency instructions without hunting through other docs.
- ❌ Avoid: Placing only a short inline question list in the study plan (e.g., "Interview Guide Structure (7–8 minutes): Q1: What are the top challenges...") with no link or version info.
- ✅ Better: In the Data Collection Plan include a named link and metadata: "Interview Guide — v1.2 — [link] — Owner: Jane Doe — Last updated: 2025-12-01". The linked doc contains full script, suggested probes and follow-ups, exact timing per segment, consent language, interviewer notes, fallback questions, and a quick "need-to-know" runbook for last-minute replacements.
- **Why**: A linked, versioned guide ensures interviewer consistency, reduces misinterpretation of intent and probes, speeds onboarding or replacements, supports auditability and replication, and preserves the study's fidelity when time is tight or team members change.

### For Surveys
- Specify distribution channels
- Target response count with justification
- Note question types and validation approach
- Detail statistical analysis methods

### Data Quality Measures
- How will you ensure response quality?
- What validation steps are included?
- How will you handle incomplete or low-quality data?

---

## Timeline Section

### Required Detail Level
- **Week-by-week breakdown** with specific activities
- **Start and end dates** for each phase
- **Dependencies** explicitly noted
- **Buffer time** built in (10-20% of total timeline)

### Phase Structure
```
Week 1 (Oct 27-Nov 2):
- Day 1-2: Participant recruitment and screening
- Day 3: Finalize interview guide
- Day 4-5: Buffer for recruitment delays

Week 2 (Nov 3-9):
- Day 1-3: Conduct 12 interviews (4 per day)
- Day 4-5: Initial transcription and review
```

### Milestone Format
- Use specific dates, not relative terms
- ❌ Avoid: "After recruitment"
- ✅ Better: "November 3: Begin interviews"

#### Include a weekly, owner-linked timeline for field studies (Learned: December 2025)
Create timelines at a weekly cadence (with key daily checkpoints and event-day hourly windows) that map activities to owners, deliverables, and contingency buffers. For intercept and conference research, this means turning a list of dated tasks into a short sprint plan that makes responsibilities, readiness checks, and fallback options explicit so team members can coordinate travel, coverage, equipment, and recruitment in the days leading up to — and during — the event.
- ❌ Avoid: Listing only specific dates and high-level tasks (e.g., "Oct 20-22: Finalize interview guide; Oct 23: Test recording equipment; Oct 26: Travel/scout") with no weekly breakdown, owners, checkpoints, or contingency time.
- ✅ Better: Provide a weekly breakdown with owners, deliverables, and checkpoints. Example:
  - Week -3 (Oct 6–12): Owner A — finalize screener/interview guide; deliverable: locked script v1; checkpoint: stakeholder review on Oct 10.
  - Week -2 (Oct 13–19): Owner B — recruit + confirm pilot participants; deliverable: recruitment list; checkpoint: pilot interviews on Oct 17.
  - Week -1 (Oct 20–26): Day-by-day tasks with owners and an equipment & logistics checklist (Oct 23: equipment dry-run; Oct 24: print field materials; Oct 25: team rehearsal; Oct 26: travel + site scouting with mapped intercept locations and hourly staffing matrix).
  - Event-day: hourly schedule and staffing rotations; backup contact and spare-equipment lead assigned.
  - Post-event: Day 1 — data backup + debrief; Days 2–7 — transcription and rapid synthesis checkpoints.
- **Why**: A weekly owner-linked timeline reduces ambiguity, surfaces risks early (recruitment shortfalls, equipment failure, travel delays), enables smoother coordination across roles, ensures adequate rehearsal and buffer time, and makes post-event workflows predictable — all of which improve data quality and reduce last-minute failures in fast-paced field studies.

---

## Participant Recruitment Section

### Criteria Specificity
- **Inclusion criteria**: Specific, measurable characteristics
- **Exclusion criteria**: Clear boundaries
- **Screening questions**: 3-5 questions to validate criteria

### Recruitment Strategy
- **Channels**: Specific platforms or methods (e.g., "LinkedIn outreach in startup founder groups")
- **Timeline**: Days allocated for recruitment
- **Backup channels**: If primary channel fails
- **Incentive structure**: Specific amounts or value

### Example Format
```
Inclusion Criteria:
- Current startup founder (verified by LinkedIn)
- Company stage: Pre-seed through Series A
- B2B or B2C software product
- Team size: 2-20 people

Exclusion Criteria:
- Solo founders without team
- Non-software businesses
- Companies beyond Series A

Screening Questions:
1. What is your current role and company?
2. What stage is your company at?
3. What type of product do you build?
```

---

## Budget & Resources Section

### Budget Breakdown Format
```
Personnel:
- Researcher time: [X hours @ $Y/hour] = $Z
- Analysis support: [X hours @ $Y/hour] = $Z

Tools & Software:
- Survey platform: $X
- Transcription service: $Y
- Analysis software: $Z

Participant Incentives:
- 12 interviews × $X per participant = $Y

Total Estimated Budget: $[TOTAL]
```

### Resource Requirements
- Specify tools needed (with costs if applicable)
- Note personnel time requirements
- Include any external services (transcription, translation, etc.)

---

## Risks & Mitigation Section

### Risk Format
For each risk, include:
- **Risk description**: What could go wrong?
- **Likelihood**: Low/Medium/High
- **Impact**: Low/Medium/High
- **Mitigation strategy**: Specific preventive actions
- **Contingency plan**: What to do if risk occurs

### Common UXR Risks to Consider
- Recruitment difficulties (can't find participants)
- Timeline delays (interviews cancelled, rescheduled)
- Data quality issues (participants don't engage deeply)
- Budget overruns (incentive costs, tool costs)
- Stakeholder misalignment (objectives shift mid-project)
- Technical failures (recording issues, data loss)

### Example Entry
```
Risk: Difficulty recruiting 12 qualified participants
- Likelihood: Medium
- Impact: High (delays entire project)
- Mitigation: Start recruitment 2 weeks early; use 3 channels simultaneously
- Contingency: Reduce sample to 8-10 if quality remains high; extend timeline by 1 week
```

---

## Success Criteria Section

### Measurable Outcomes
Each criterion must be:
- **Specific**: Exactly what success looks like
- **Measurable**: How you'll know if achieved
- **Observable**: Can be verified objectively

### Quality Indicators
- Research quality (depth of insights, validity)
- Process quality (timeline adherence, stakeholder satisfaction)
- Impact quality (decision influence, actionability)

### Example Format
```
Research Quality:
- Identify at least 3 distinct patterns across interviews
- Achieve thematic saturation (no new themes in final 2 interviews)
- All findings supported by quotes from 3+ participants

Process Quality:
- Complete data collection within 2-week window
- Deliver final report within 4 weeks of project start
- Stakeholder rates project communication as 4/5 or higher

Impact Quality:
- Final report includes 5+ actionable recommendations
- Insights directly inform product roadmap decisions
- Findings validated by 2+ stakeholder teams
```

---

## Document Formatting

### Section Headers
- Use clear hierarchy (H1 for main sections, H2 for subsections)
- Number main sections for easy reference
- Use consistent formatting throughout

### Lists and Bullets
- Use bullets for non-sequential items
- Use numbers for sequential steps or prioritized items
- Keep parallel structure in bullet lists

### Tables
- Use tables for structured comparisons
- Include headers for all columns
- Keep cells concise

### Visual Elements
- Consider timeline visualizations for complex schedules
- Use callout boxes for critical information
- Highlight key numbers and dates

---

## Common Pitfalls to Avoid

### Vague Timelines
- ❌ "We'll conduct interviews over a few weeks"
- ✅ "Week 1-2 (Oct 27-Nov 9): Conduct 12 interviews (4 per day on Days 1-3 of each week)"

### Unclear Sample Justification
- ❌ "We'll interview users"
- ✅ "We'll interview 12 founders (6 pre-seed, 6 seed-stage) to achieve thematic saturation while staying within budget"

### Missing Risk Planning
- ❌ No risks section, or generic risks only
- ✅ Specific project risks with concrete mitigation plans

### Unmeasurable Objectives
- ❌ "Understand user needs better"
- ✅ "Identify top 3 unmet needs related to UX research access, validated by 5+ founders"

### Budget Without Context
- ❌ "$5,000 total budget"
- ✅ "$5,000 total ($2,400 incentives, $1,500 researcher time, $600 tools, $500 buffer)"

---

## Learning Log

### Project: [To be populated by feedback-classifier]
**Date**: [Auto-populated]
**Feedback Source**: [Google Doc comments / Retrospective / User correction]
**Pattern Identified**: [Specific learning]
**Applied To Section**: [Which section of study plan]

---

## Version History

**v1.0** - Initial patterns (baseline best practices)
- Established core structure and formatting guidelines
- Defined minimum specificity requirements
- Set quality standards for each section

**Future versions will be appended here as patterns are learned from projects**

---

*This file is continuously updated by the feedback-classifier skill after each project review.*
