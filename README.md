# UXR Workflow Skills for Claude Code

> Professional UXR workflow automation using Claude Code Skills with multi-LLM planning and automatic learning system

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Skills: 4](https://img.shields.io/badge/Skills-4-green.svg)](skills/)

## What is This?

A Claude Code plugin containing 4 production-ready skills for automating end-to-end UXR workflows:

- **study-planner**: Multi-LLM workflow (Gemini-3 → ChatGPT-5 → Claude) for comprehensive research planning
- **interview-guide-writer**: Transform research plans into ready-to-use interview guides with best practices
- **feedback-learner**: Automatically extract and apply learnings from feedback using LEARN keyword system
- **skill-creator**: Create new Claude Code skills with validation utilities

## Why Use These Skills?

- **Multi-LLM Planning**: Leverage 3 different AI models for comprehensive study plans
- **Production-Ready**: Battle-tested in real UXR projects
- **Learning System**: Skills improve automatically from your feedback
- **No Database Needed**: Learning stored in simple markdown files
- **One-Command Install**: Install via `/plugin` commands
- **Automatic Updates**: Get improvements via `/plugin update`

## Quick Start

### Prerequisites

- [Claude Code](https://claude.ai/code)
- Google Workspace account
- Python 3.8+ (for skill-creator utilities)

### Installation (2 Steps)

**Step 1: Add the marketplace**
```bash
/plugin marketplace add MulanLLL/uxr_plugins
```

**Step 2: Install the plugin**
```bash
/plugin install uxr-workflow-skills@MulanLLL
```

**Step 3: Configure MCP servers** (one-time setup)

The skills require Google Workspace MCP and Zen MCP. See setup guides:
- [MCP Setup Guide](docs/MCP_SETUP.md) - Required for Google Workspace integration
- [Learning System](docs/LEARNING_SYSTEM.md) - How the LEARN keyword works

Done! All 4 skills are now available.

## Skills Catalog

### 1. study-planner

**Purpose**: Creates comprehensive UXR study plans using validated 3-step multi-LLM workflow

**When to use**: Starting new UXR project, need detailed research plan

**Workflow**:
- Step 1: Gemini-3 (Principal Researcher) - Strategic vision and narrative
- Step 2: ChatGPT-5 (Research Ops) - Methodological rigor and feasibility  
- Step 3: Claude (Lead Researcher) - Synthesis and industry validation

**Dependencies**:
- MCP: google-workspace (for creating Google Docs)
- MCP: zen (for multi-LLM access)
- Skill: feedback-learner (for learning extraction)

**Example usage**:
```
User: "Create a study plan for researching startup founders' needs for UX insights"

Claude (study-planner activates):
1. Asks context questions
2. Executes 3-step workflow
3. Creates Google Doc in Planning/ folder
4. Shares link for review
```

---

### 2. interview-guide-writer

**Purpose**: Transforms research plans into ready-to-use interview guides

**When to use**: After study plan approval, before participant recruitment

**Features**:
- Opening and closing scripts
- Consent and privacy language
- Core questions with probes and timing guidance
- Field notes templates
- Participant tracking sheets
- Multiple guide strategies (Guide A/B alternating)

**Dependencies**:
- MCP: google-workspace
- References: interview_best_practices.md (462 lines of best practices)

**Example usage**:
```
User: "Create interview guide based on the study plan"

Claude (interview-guide-writer activates):
1. Reads study plan from Google Drive
2. Extracts research questions
3. Creates comprehensive interview guide
4. Saves to Interviews/ folder
```

---

### 3. feedback-learner

**Purpose**: Automatically extracts learnings from Google Doc comments marked with LEARN keyword

**When to use**: Automatically activates when you say "I've added comments"

**How it works**:
1. You review skill output in Google Docs
2. Add comments with **"LEARN"** (all caps) for patterns to remember
3. Add regular comments (no LEARN) for project-specific feedback
4. Tell Claude "I've added comments"
5. Skill auto-activates, filters LEARN comments, generalizes learnings
6. Next project automatically applies learnings

**Why LEARN keyword**: Prevents overgeneralization - explicit control over what becomes learned knowledge

**Dependencies**:
- MCP: google-workspace (read comments, document content)
- MCP: zen (LLM generalization via Gemini-3)

**Example**:
```
First Project:
Comment: "LEARN: Too vague"
On text: "Timeline: 4 weeks"

→ Generalized: "Include weekly timeline with specific milestones"
→ Saved to: study-planner/references/learnings.md

Second Project:
→ Study plan automatically includes detailed weekly timeline
```

---

### 4. skill-creator

**Purpose**: Guide and utilities for creating new Claude Code skills

**When to use**: Creating custom skills for your workflow

**Features**:
- `init_skill.py` - Generate new skill templates
- `package_skill.py` - Validate and package skills
- `quick_validate.py` - Fast validation checks
- Progressive disclosure architecture guidance

**Dependencies**: None (standalone utilities)

**Example usage**:
```
User: "Help me create a new skill for data analysis"

Claude (skill-creator activates):
1. Guides through skill structure
2. Provides templates and examples
3. Validates created skills
```

## How the Learning System Works

The learning system is the core innovation. Here's the complete workflow:

### 1. User Reviews Output

After a skill creates a document, you review it and add comments:
- Comments with **"LEARN"** (all caps) → Become stored learnings
- Regular comments (without LEARN) → Project-specific feedback only

### 2. Automatic Learning Extraction

When you say "I've added comments", feedback-learner:
1. Reads all comments from Google Doc
2. Filters for LEARN keyword (case-sensitive)
3. Extracts context (quoted text, section, surrounding paragraphs)
4. Generalizes via LLM (Gemini-3 as UX principal researcher)
5. Identifies source skill based on folder location
6. Shows extracted learnings for confirmation
7. Saves to skill's learnings.md
8. Auto-resolves LEARN comments

### 3. Automatic Application

Next time the skill runs:
1. Reads learnings.md automatically
2. Applies all learned patterns
3. No manual reminder needed

**Why This Matters**: One-time feedback becomes permanent improvement across all future projects.

See [docs/LEARNING_SYSTEM.md](docs/LEARNING_SYSTEM.md) for complete documentation.

## Installation Methods

### Method 1: Plugin Installation (Recommended)

```bash
# Add marketplace
/plugin marketplace add MulanLLL/uxr_plugins

# Install plugin
/plugin install uxr-workflow-skills@MulanLLL

# Verify installation
/plugin
# Navigate to "Installed" tab to see uxr-workflow-skills
```

**Update to latest version**:
```bash
/plugin marketplace update MulanLLL
/plugin update uxr-workflow-skills@MulanLLL
```

### Method 2: Manual Installation (Alternative)

```bash
# Clone repository
git clone https://github.com/MulanLLL/uxr_plugins.git
cd uxr_plugins

# Copy all skills
cp -r skills/* ~/.claude/skills/
```

**Note**: Manual installation doesn't benefit from automatic updates.

## Documentation

- [Getting Started Guide](docs/GETTING_STARTED.md) - Quick start walkthrough
- [Installation Guide](docs/INSTALLATION.md) - Detailed setup instructions
- [MCP Setup Guide](docs/MCP_SETUP.md) - Google Workspace & Zen MCP configuration
- [Learning System](docs/LEARNING_SYSTEM.md) - How LEARN keyword works
- [Skills Overview](docs/SKILLS_OVERVIEW.md) - Complete skills catalog
- [Workflows](docs/WORKFLOWS.md) - End-to-end UXR workflows
- [FAQ](docs/FAQ.md) - Common questions
- [Troubleshooting](docs/TROUBLESHOOTING.md) - Common issues

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Quick contribution workflow:
1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-improvement`
3. Make your changes
4. Test thoroughly
5. Submit pull request

**Ways to contribute**:
- Improve existing skills (add learnings, fix bugs, enhance docs)
- Share your accumulated learnings via pull request
- Report issues or suggest features
- Improve documentation

## License

Apache License 2.0 - See [LICENSE](LICENSE) for details.

You can:
- Use commercially
- Modify and distribute
- Sublicense

You must:
- Include license and copyright notice
- State changes made

## Support

- **Issues**: [GitHub Issues](https://github.com/MulanLLL/uxr_plugins/issues)
- **Discussions**: [GitHub Discussions](https://github.com/MulanLLL/uxr_plugins/discussions)

## Acknowledgments

Built with:
- [Claude Code](https://claude.ai/code) by Anthropic
- [Google Workspace MCP Server](https://github.com/modelcontextprotocol/servers)
- [Zen MCP Server](https://github.com/BeehiveInnovations/zen-mcp-server)

---

**Happy researching! 📋✨**
