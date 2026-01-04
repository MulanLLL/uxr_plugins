# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0] - 2026-01-03

### Added

#### Core Plugin Infrastructure
- Initial public release of UXR Workflow Skills plugin
- `.claude-plugin/plugin.json` manifest for `/plugin` command installation
- Apache License 2.0
- Comprehensive README.md with installation instructions and learning system documentation
- CONTRIBUTING.md with contribution guidelines and code standards
- .gitignore with security exclusions for learnings.md and credentials

#### Skills Included

**study-planner (v1.0.0)**
- Multi-LLM workflow (Gemini-3 → ChatGPT-5 → Claude) for comprehensive research planning
- Creates study plans in Google Docs via MCP
- Includes 355 lines of learnings template with best practices
- 3-step workflow: Principal Researcher → Research Ops → Lead Researcher
- Human review and revision loop integration
- Automatic learning extraction from Google Doc comments

**interview-guide-writer (v1.0.0)**
- Transforms research plans into ready-to-use interview guides
- 462 lines of interview best practices reference
- Field notes template (2362 bytes)
- Participant tracking template (1380 bytes)
- Creates guides in Google Docs with proper structure
- Supports multiple guide strategies (Guide A/B alternating)

**feedback-learner (v1.0.0)**
- LEARN keyword system for automatic learning extraction
- Reads Google Doc comments and filters for LEARN markers
- Context-aware learning extraction (quoted text, section, surrounding paragraphs)
- Generalizes learnings via LLM (Gemini-3 as UX principal researcher)
- Folder-based skill identification
- Auto-resolves LEARN comments after extraction
- Updates skill learnings.md files automatically

**skill-creator (v1.0.0)**
- Guide for creating new Claude Code skills
- `init_skill.py` - Generate new skill templates
- `package_skill.py` - Validate and package skills
- `quick_validate.py` - Fast validation checks
- Progressive disclosure architecture guidance
- Skill structure templates and examples

#### Documentation
- docs/GETTING_STARTED.md - Quick start walkthrough
- docs/INSTALLATION.md - Detailed setup instructions
- docs/MCP_SETUP.md - Google Workspace & Zen MCP configuration
- docs/LEARNING_SYSTEM.md - LEARN keyword system documentation
- docs/SKILLS_OVERVIEW.md - Complete skills catalog
- docs/WORKFLOWS.md - End-to-end UXR workflows
- docs/FAQ.md - Frequently asked questions
- docs/TROUBLESHOOTING.md - Common issues and solutions

#### Examples
- examples/study_plan_example.md - Example study plan output
- examples/interview_guide_example.md - Example interview guide
- examples/full_workflow_example.md - Complete workflow demonstration

### Dependencies

#### Required
- Claude Code (claude.ai/code)
- Google Workspace account

#### MCP Servers
- google-workspace (for Docs, Sheets, Drive, Calendar, Tasks operations)
- zen (for multi-LLM access - required only for study-planner)

#### Optional
- Python 3.8+ (for skill-creator validation utilities)

### Installation

Users can install via plugin commands:

```bash
# Add marketplace
/plugin marketplace add MulanLLL/uxr_plugins

# Install plugin
/plugin install uxr-workflow-skills@MulanLLL/uxr_plugins
```

Or manually:

```bash
git clone https://github.com/MulanLLL/uxr_plugins.git
cp -r uxr_plugins/skills/* ~/.claude/skills/
```

### Notes

- This is the first public release
- All skills have been battle-tested in real UXR projects
- Learning system uses LEARN keyword filtering for precise control
- No database required - all learnings stored in markdown files
- Plugin structure validated with `/plugin validate`

---

## Version History

- **1.0.0** (2026-01-03) - Initial public release

---

## Future Roadmap

### Planned Features (Post 1.0.0)

- **survey-creator**: Generate survey questionnaires in Google Docs
- **survey-programmer**: Program surveys in Google Forms with Python API
- **data-analyzer**: Analyze qualitative and quantitative research data
- **report-generator**: Create comprehensive research reports
- **doc-formatter**: Polish Google Docs with professional formatting
- **recruitment-helper**: Create screeners and outreach materials

### Potential Enhancements

- Additional best practices references for each skill
- More comprehensive learnings templates
- Video tutorials and demos
- Integration with additional MCP servers
- Community-contributed learnings repository

---

## Upgrade Guide

### From Development to 1.0.0

If you've been using skills locally before the plugin release:

1. **Backup your learnings**:
   ```bash
   cp ~/.claude/skills/study-planner/references/learnings.md ~/backup/
   cp ~/.claude/skills/interview-guide-writer/references/learnings.md ~/backup/
   cp ~/.claude/skills/feedback-learner/references/learnings.md ~/backup/
   cp ~/.claude/skills/skill-creator/references/learnings.md ~/backup/
   ```

2. **Install via plugin**:
   ```bash
   /plugin marketplace add MulanLLL/uxr_plugins
   /plugin install uxr-workflow-skills@MulanLLL/uxr_plugins
   ```

3. **Restore your learnings**:
   ```bash
   cp ~/backup/learnings.md ~/.claude/skills/study-planner/references/
   cp ~/backup/learnings.md ~/.claude/skills/interview-guide-writer/references/
   # ... repeat for other skills
   ```

---

## Feedback and Issues

- **Bug Reports**: [GitHub Issues](https://github.com/MulanLLL/uxr_plugins/issues)
- **Feature Requests**: [GitHub Discussions](https://github.com/MulanLLL/uxr_plugins/discussions)
- **Contributions**: See [CONTRIBUTING.md](CONTRIBUTING.md)

---

[Unreleased]: https://github.com/MulanLLL/uxr_plugins/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/MulanLLL/uxr_plugins/releases/tag/v1.0.0
