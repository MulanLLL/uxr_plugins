# study-planner

> Creates comprehensive UXR study plans using validated 3-step multi-LLM workflow

## Overview

The study-planner skill generates detailed user research study plans through a sophisticated 3-step multi-LLM workflow that combines strategic vision, methodological rigor, and industry validation. Each plan is created in Google Docs and saved to your Google Drive for easy collaboration and review.

**Multi-LLM Workflow**:
1. **Step 1: Gemini-3 (Principal Researcher)** - Creates strategic narrative and research vision
2. **Step 2: ChatGPT-5 (Research Ops)** - Adds methodological rigor and feasibility analysis  
3. **Step 3: Claude (Lead Researcher)** - Synthesizes insights with industry validation

This approach ensures study plans are strategically sound, operationally feasible, and aligned with industry best practices.

## When to Use

**Trigger Phrases**:
- "Create a study plan for [research topic]"
- "I need a research plan for [project]"
- "Start planning UXR study about [topic]"
- "Generate study plan for [objective]"

**Use Cases**:
- Starting a new UXR project
- Planning research for product features
- Creating research proposals
- Designing academic UX studies
- Planning mixed-method research (surveys + interviews)

## Features

### Core Capabilities

- **Multi-LLM Synthesis**: Combines strengths of 3 different AI models
- **Human Review Loop**: Built-in revision process with feedback integration
- **Learning System**: Automatically improves from your feedback via LEARN keyword
- **Google Drive Integration**: Creates plans directly in Google Docs via MCP
- **Comprehensive Structure**: Includes all essential study plan sections
- **Best Practices**: 355 lines of accumulated learnings and patterns

### Study Plan Sections

Generated plans typically include:

- **Executive Summary**: Project overview and key objectives
- **Research Questions**: Specific, answerable research inquiries
- **Methodology**: Detailed approach (interviews, surveys, or mixed-method)
- **Timeline**: Week-by-week schedule with specific milestones
- **Participant Criteria**: Target audience and recruitment requirements
- **Deliverables**: Expected outputs and artifacts
- **Success Metrics**: How to measure research impact
- **Risks and Mitigation**: Potential challenges and solutions

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
cp -r uxr_plugins/skills/study-planner ~/.claude/skills/
```

## Dependencies

### Required

- **Claude Code**: Main platform (claude.ai/code)
- **Google Workspace Account**: For creating Google Docs
- **Google Workspace MCP Server**: For Docs and Drive operations

### Optional

- **Zen MCP Server**: For multi-LLM access (Gemini-3, ChatGPT-5, Claude)
  - Required for full 3-step workflow
  - Without Zen MCP, skill falls back to Claude-only mode

See [docs/MCP_SETUP.md](../../docs/MCP_SETUP.md) for configuration instructions.

## Usage

### Basic Workflow

1. **Trigger the skill**:
   ```
   User: "Create a study plan for researching mobile app onboarding"
   ```

2. **Provide context**:
   Claude will ask clarifying questions about:
   - Research objectives
   - Target audience
   - Methodology preferences (interviews, surveys, or both)
   - Timeline constraints
   - Key stakeholders

3. **Review generated plan**:
   - Claude creates plan in Google Doc
   - Shares link for review
   - Plan is saved in Google Drive Planning/ folder

4. **Provide feedback**:
   - Add comments directly in Google Doc
   - Use "LEARN" keyword for patterns to remember
   - Tell Claude "I've added comments"
   - feedback-learner extracts learnings automatically

5. **Iterate until approved**:
   - Claude revises based on feedback
   - Process repeats until you approve

### Example Conversation

```
User: "Create a study plan for researching how freelancers manage their finances"

Claude: I'll help you create a comprehensive study plan. Let me ask a few questions:

1. What are your primary research objectives?
2. Who is your target audience (specific freelancer segments)?
3. What methodology are you considering (interviews, surveys, or both)?
4. What's your target timeline?
5. Any specific constraints or requirements?

User: 
1. Understand pain points in financial management
2. Freelancers earning $50k-150k annually
3. Mixed method - surveys for breadth, interviews for depth
4. 8 weeks total
5. Need to present to stakeholders by end of Q1

Claude: Thank you! I'll create a comprehensive study plan using our multi-LLM workflow.

[Executes 3-step workflow]
[Creates Google Doc]

I've created your study plan here: [Google Doc link]

The plan includes:
- 8-week timeline with weekly milestones
- Mixed-method approach (survey n=200, interviews n=15)
- Detailed research questions
- Participant recruitment strategy
- Stakeholder presentation timeline

Please review and let me know if you'd like any changes!

User: I've added comments in the doc

Claude: [feedback-learner activates automatically]
I've extracted 3 learnings from your comments:
1. Include specific sample sizes in methodology section
2. Add budget breakdown for participant incentives
3. Specify deliverable formats (slides vs document)

I'll update the plan now...

[Revises and presents updated version]
```

## Configuration

### Customizing Learnings Template

The skill includes a learnings template at `references/learnings_template.md` with 355 lines of best practices. You can customize this for your organization:

1. **Backup original**:
   ```bash
   cp ~/.claude/skills/study-planner/references/learnings_template.md ~/backup/
   ```

2. **Add organization-specific patterns**:
   ```markdown
   ## Stakeholder Section
   - Always include [specific stakeholder role] in distribution list
   - Use [company-specific] terminology for methodologies
   ```

3. **Test changes**:
   Create a new study plan and verify your patterns are applied

### Learning from Feedback

To teach the skill new patterns:

1. Review generated study plan in Google Docs
2. Add comments with "LEARN" keyword (all caps):
   - ✅ "LEARN: Add weekly status update section"
   - ✅ "LEARN this for future: Include stakeholder matrix"
   - ❌ "learn this" (lowercase - won't be extracted)

3. Tell Claude "I've added comments"
4. feedback-learner extracts and generalizes learnings
5. Next study plan automatically applies the pattern

See [docs/LEARNING_SYSTEM.md](../../docs/LEARNING_SYSTEM.md) for complete documentation.

## Examples

### Example 1: Mobile App Research

**Request**: "Create a study plan for improving mobile app navigation"

**Output**: 
- Research questions focused on navigation pain points
- Mixed-method approach (survey + usability testing)
- 6-week timeline
- Deliverable: Redesign recommendations

### Example 2: B2B SaaS Research

**Request**: "Plan research on enterprise software adoption barriers"

**Output**:
- Interview-focused methodology (decision-makers and end users)
- 10-week timeline with stakeholder check-ins
- Risk mitigation for access to enterprise participants
- Deliverable: Executive summary and detailed findings

### Example 3: Academic Research

**Request**: "Create study plan for thesis on AR interface design"

**Output**:
- Literature review phase
- Mixed-method with controlled experiments
- 16-week academic timeline
- IRB compliance considerations
- Deliverable: Thesis chapters and conference paper

See [examples/study_plan_example.md](../../examples/study_plan_example.md) for full example output.

## Troubleshooting

### Common Issues

**Issue**: "MCP server not found"
- **Solution**: Ensure Google Workspace MCP is installed and connected
- **Check**: Restart Claude Code after MCP installation

**Issue**: "Zen MCP not available - falling back to Claude-only"
- **Solution**: Install Zen MCP for multi-LLM workflow (optional)
- **Alternative**: Claude-only mode still produces high-quality plans

**Issue**: "Cannot create Google Doc"
- **Solution**: Verify Google Workspace MCP authentication
- **Check**: Try creating a doc manually via MCP to test connection

**Issue**: "Learnings not being applied"
- **Solution**: Verify learnings.md exists in references/ folder
- **Check**: Ensure LEARN comments use all caps keyword

**Issue**: "Plan missing expected sections"
- **Solution**: Add specific requirements in initial prompt
- **Example**: "Create study plan including budget section"

### Getting Help

- **Documentation**: [docs/TROUBLESHOOTING.md](../../docs/TROUBLESHOOTING.md)
- **Issues**: [GitHub Issues](https://github.com/MulanLLL/uxr_plugins/issues)
- **Discussions**: [GitHub Discussions](https://github.com/MulanLLL/uxr_plugins/discussions)

## Technical Details

### File Structure

```
study-planner/
├── SKILL.md                           # 572 lines - Skill definition
├── README.md                          # This file
└── references/
    └── learnings_template.md          # 355 lines - Best practices
```

### Workflow Architecture

```
User Input → Context Questions
    ↓
Step 1: Gemini-3 (Principal Researcher)
    ↓
Step 2: ChatGPT-5 (Research Ops)
    ↓
Step 3: Claude (Lead Researcher)
    ↓
Google Doc Creation → User Review
    ↓
Feedback Loop → Learning Extraction
    ↓
Approved Plan
```

### Learning System Integration

The skill automatically:
1. Reads `references/learnings.md` before generating plans
2. Applies all learned patterns
3. Integrates with feedback-learner for automatic learning extraction
4. Updates learnings.md when LEARN comments are processed

## Version History

- **v1.0.0** (2026-01-03): Initial release with multi-LLM workflow and 355-line learnings template

## Contributing

We welcome contributions! Ways to help:

- **Share learnings**: Contribute patterns you've discovered
- **Improve documentation**: Clarify instructions or add examples
- **Report issues**: Help us identify bugs or edge cases
- **Enhance workflow**: Suggest improvements to the 3-step process

See [CONTRIBUTING.md](../../CONTRIBUTING.md) for guidelines.

## License

Apache License 2.0 - See [LICENSE](../../LICENSE) for details.

---

**Part of the UXR Workflow Skills plugin** | [Main Documentation](../../README.md)
