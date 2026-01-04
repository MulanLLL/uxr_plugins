# interview-guide-writer

> Transforms research plans into ready-to-use interview guides with best practices

## Overview

The interview-guide-writer skill generates comprehensive, professional interview guides based on your research plan. Each guide includes opening and closing scripts, consent language, core questions with probes, timing guidance, and field notes templates—everything you need to conduct effective user research interviews.

The skill automatically reads your study plan from Google Drive, extracts research questions, and creates a structured interview guide optimized for your methodology.

## When to Use

**Trigger Phrases**:
- "Create interview guide based on the study plan"
- "Generate interview questions for [research topic]"
- "I need an interview guide for [project]"
- "Build interview script from the research plan"

**Use Cases**:
- After study plan approval, before participant recruitment
- Creating guides for user interviews
- Designing stakeholder interview scripts
- Building guides for usability testing sessions
- Planning structured or semi-structured interviews

## Features

### Core Capabilities

- **Study Plan Integration**: Automatically reads approved research plan
- **Complete Interview Scripts**: Opening, closing, consent, and transitions
- **Question Hierarchy**: Core questions with follow-up probes
- **Timing Guidance**: Duration estimates for each section
- **Field Notes Templates**: Structured note-taking forms
- **Participant Tracking**: Spreadsheet for managing interview sessions
- **Best Practices Built-In**: 462 lines of interview methodology expertise
- **Multiple Guide Strategies**: Guide A/B alternating for consistency checks

### Interview Guide Sections

Generated guides typically include:

- **Opening Script**: Warm welcome and rapport building
- **Consent and Privacy**: Recording, confidentiality, and rights
- **Research Context**: Study purpose and participant role
- **Core Questions**: Research questions with timing
- **Follow-up Probes**: Deeper exploration prompts
- **Closing Script**: Thank you and next steps
- **Field Notes Template**: Structured observation recording
- **Participant Tracker**: Session management spreadsheet

## Installation

The skill is automatically installed when you install the uxr-workflow-skills plugin:

```bash
# Install via plugin commands
/plugin marketplace add MulanLLL/uxr_plugins
/plugin install uxr-workflow-skills@MulanLLL/uxr_plugins
```

Manual installation (alternative):

```bash
# Clone repository
git clone https://github.com/MulanLLL/uxr_plugins.git

# Copy skill to Claude Code skills directory
cp -r uxr_plugins/skills/interview-guide-writer ~/.claude/skills/
```

## Dependencies

### Required

- **Claude Code**: Main platform (claude.ai/code)
- **Google Workspace Account**: For accessing study plans and creating guides
- **Google Workspace MCP Server**: For Docs and Drive operations

### References

- **interview_best_practices.md**: 462 lines of interview methodology best practices
- **field_notes_template.md**: Structured template for session notes (2362 bytes)

See [docs/MCP_SETUP.md](../../docs/MCP_SETUP.md) for MCP configuration.

## Usage

### Basic Workflow

1. **Ensure study plan exists**:
   - Must have approved study plan in Google Drive
   - Located in Planning/ folder (created by study-planner skill)

2. **Trigger the skill**:
   ```
   User: "Create interview guide based on the study plan"
   ```

3. **Provide study plan location**:
   - Claude will search for study plan in Google Drive
   - Or you can provide the Google Doc URL directly

4. **Review generated guide**:
   - Claude creates guide in Google Doc
   - Shares link for review
   - Guide is saved in Interviews/ folder

5. **Provide feedback and iterate**:
   - Add comments in Google Doc
   - Use "LEARN" keyword for patterns to remember
   - Tell Claude "I've added comments"
   - Iterate until approved

### Example Conversation

```
User: "Create interview guide from the freelancer finance study plan"

Claude: I'll search for your study plan in Google Drive...

Found: "Freelancer Financial Management - Study Plan"

I'll create a comprehensive interview guide based on this plan. The guide will include:
- Opening script and consent language
- 8 core questions based on your research questions
- Follow-up probes for deeper exploration
- 45-minute timing structure (as specified in plan)
- Field notes template
- Participant tracking sheet

[Reads study plan]
[Creates interview guide]

I've created your interview guide here: [Google Doc link]

The guide includes:
- Warm opening with informed consent (5 min)
- Background questions (5 min)
- Core questions on financial pain points (25 min)
- Tool and workflow questions (10 min)
- Closing and next steps (5 min)
- Field notes template for observations
- Participant tracker (ready for 15 interviews as planned)

Please review and let me know if you'd like any changes!

User: I've added comments

Claude: [feedback-learner activates]
I've extracted 2 learnings:
1. Add specific probes about tool integrations
2. Include section for unexpected insights

I'll update the guide now...

[Revises and presents updated version]
```

## Configuration

### Customizing Best Practices

The skill includes extensive best practices at `references/interview_best_practices.md` (462 lines). You can add organization-specific practices:

1. **Review current practices**:
   ```bash
   cat ~/.claude/skills/interview-guide-writer/references/interview_best_practices.md
   ```

2. **Add your practices**:
   Edit the file to include company-specific approaches:
   ```markdown
   ## Company-Specific Practices
   - Always mention NDA requirements in opening
   - Use standardized compensation language
   - Include diversity and inclusion statement
   ```

### Customizing Templates

**Field Notes Template** (`assets/field_notes_template.md`):
- Modify sections for your research focus
- Add custom observation categories
- Include specific data collection requirements

### Learning from Feedback

To teach the skill new patterns:

1. Review interview guide in Google Docs
2. Add comments with "LEARN" keyword:
   - ✅ "LEARN: Add time buffer between questions"
   - ✅ "LEARN this: Include warmup question before sensitive topics"

3. Tell Claude "I've added comments"
4. feedback-learner extracts learnings automatically
5. Next guide automatically applies the pattern

## Examples

### Example 1: User Interview Guide

**Input**: Study plan for mobile banking app research

**Output**:
- 60-minute interview structure
- Questions on current banking behaviors
- Probes for pain points and workarounds
- Prototype testing section (if applicable)
- Closing with feature prioritization exercise

### Example 2: Stakeholder Interview Guide

**Input**: Study plan for enterprise software evaluation

**Output**:
- 45-minute structured interview
- Questions on decision criteria and processes
- Probes for organizational constraints
- Budget and timeline exploration
- Success metrics definition

### Example 3: Usability Testing Guide

**Input**: Study plan for website navigation study

**Output**:
- 30-minute moderated test structure
- Task scenarios with success criteria
- Think-aloud protocol instructions
- Observation framework
- Post-test satisfaction questions

See [examples/interview_guide_example.md](../../examples/interview_guide_example.md) for full example output.

## Troubleshooting

### Common Issues

**Issue**: "Cannot find study plan"
- **Solution**: Ensure study plan exists in Google Drive Planning/ folder
- **Alternative**: Provide direct Google Doc URL

**Issue**: "Questions don't match research objectives"
- **Solution**: Verify study plan has clear research questions section
- **Check**: Review generated questions and provide specific feedback

**Issue**: "Missing field notes template"
- **Solution**: Check assets/ folder exists with templates
- **Fix**: Reinstall skill or copy templates manually

**Issue**: "Interview timing doesn't match requirements"
- **Solution**: Specify duration in initial prompt
- **Example**: "Create 30-minute interview guide"

**Issue**: "Consent language not appropriate for my region"
- **Solution**: Add LEARN comment with region-specific requirements
- **Example**: "LEARN: Include GDPR-compliant consent for EU studies"

### Getting Help

- **Documentation**: [docs/TROUBLESHOOTING.md](../../docs/TROUBLESHOOTING.md)
- **Issues**: [GitHub Issues](https://github.com/MulanLLL/uxr_plugins/issues)
- **Discussions**: [GitHub Discussions](https://github.com/MulanLLL/uxr_plugins/discussions)

## Technical Details

### File Structure

```
interview-guide-writer/
├── SKILL.md                                    # 278 lines - Skill definition
├── README.md                                   # This file
├── references/
│   ├── interview_best_practices.md             # 462 lines - Methodology expertise
│   └── learnings_template.md                   # Learning examples
└── assets/
    └── field_notes_template.md                 # 2362 bytes - Session notes
```

### Workflow Architecture

```
User Request → Study Plan Search
    ↓
Read Study Plan → Extract Research Questions
    ↓
Apply Best Practices → Apply Learnings
    ↓
Generate Interview Guide Structure
    ↓
Create Google Doc → Add Templates
    ↓
User Review → Feedback Loop
    ↓
Approved Guide
```

### Best Practices Integration

The skill automatically applies:
- Opening and closing scripts best practices
- Consent language standards
- Question ordering principles
- Probe design patterns
- Timing estimation rules
- Note-taking structures

### Learning System Integration

The skill:
1. Reads `references/learnings.md` before generating guides
2. Applies learned question patterns
3. Integrates with feedback-learner for extraction
4. Updates learnings.md via LEARN comments

## Interview Guide Strategies

### Guide A/B Alternating

For consistency checking across interviews, the skill can create two guide versions:

**Guide A**: Standard question order
**Guide B**: Alternate question order (same content, different sequence)

This helps identify:
- Order effects in responses
- Question dependency issues
- Priming or anchoring effects

Request this feature by saying: "Create Guide A and Guide B versions"

## Best Practices Reference

The 462-line best practices reference includes:

- **Opening Techniques**: Building rapport and setting context
- **Question Design**: Open-ended, neutral, focused questions
- **Probe Strategies**: Deepening exploration without leading
- **Active Listening**: Techniques for attentive interviewing
- **Handling Difficult Moments**: Silence, emotion, confusion
- **Closing Well**: Gratitude, next steps, maintaining relationship
- **Note-Taking**: Structured observation frameworks
- **Ethics**: Consent, privacy, participant rights

## Version History

- **v1.0.0** (2026-01-03): Initial release with 462-line best practices and templates

## Contributing

We welcome contributions! Ways to help:

- **Share best practices**: Contribute interview techniques
- **Improve templates**: Enhance field notes or tracking templates
- **Add examples**: Share successful guide structures
- **Report issues**: Help identify gaps or errors

See [CONTRIBUTING.md](../../CONTRIBUTING.md) for guidelines.

## License

Apache License 2.0 - See [LICENSE](../../LICENSE) for details.

---

**Part of the UXR Workflow Skills plugin** | [Main Documentation](../../README.md)
