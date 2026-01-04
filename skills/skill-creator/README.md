# skill-creator

> Guide and utilities for creating new Claude Code skills with validation

## Overview

The skill-creator provides comprehensive guidance and Python utilities for creating new Claude Code skills following best practices. Whether you're building skills for your own workflow or contributing to the UXR Workflow Skills plugin, this skill helps ensure your skills are well-structured, documented, and functional.

**Included Utilities**:
- `init_skill.py` - Generate new skill templates
- `package_skill.py` - Validate and package skills for distribution
- `quick_validate.py` - Fast validation checks during development

## When to Use

**Trigger Phrases**:
- "Help me create a new skill for [purpose]"
- "I want to build a skill that [does X]"
- "Guide me through creating a Claude Code skill"
- "Validate my skill structure"

**Use Cases**:
- Creating custom skills for your workflow
- Contributing new skills to this plugin
- Learning skill development best practices
- Validating existing skills
- Packaging skills for distribution

## Features

### Core Capabilities

- **Skill Templates**: Pre-built structure for quick starts
- **Best Practices Guidance**: Progressive disclosure architecture
- **Validation Tools**: Automated structure and content checks
- **Packaging Utilities**: Prepare skills for sharing
- **Documentation Templates**: README and learnings templates
- **SKILL.md Examples**: Reference implementations

### Progressive Disclosure Architecture

Skills should reveal information progressively:

**Level 1: Metadata** (YAML frontmatter)
- name, description, version
- triggers, dependencies
- Loaded immediately by Claude Code

**Level 2: Core Instructions**
- Essential workflow steps
- Required context
- Loaded when skill activates

**Level 3: Extended Context** 
- Best practices references
- Learnings files
- Loaded as needed

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
cp -r uxr_plugins/skills/skill-creator ~/.claude/skills/
```

## Dependencies

### Required

- **Claude Code**: Main platform (claude.ai/code)
- **Python 3.8+**: For validation and packaging utilities

### Optional

- **Google Workspace MCP**: If your skill creates Docs/Sheets/Forms
- **Other MCP servers**: Depending on skill functionality

## Usage

### Creating a New Skill

#### Method 1: Using init_skill.py

```bash
# Navigate to skills directory
cd ~/.claude/skills/

# Run init_skill.py
python skill-creator/scripts/init_skill.py my-new-skill

# Creates structure:
# my-new-skill/
# ├── SKILL.md
# ├── README.md
# └── references/
#     └── learnings_template.md
```

#### Method 2: Manual Creation

1. **Create directory structure**:
   ```bash
   mkdir -p ~/.claude/skills/my-new-skill/references
   ```

2. **Create SKILL.md**:
   ```yaml
   ---
   name: my-new-skill
   description: Brief description of what this skill does
   version: 1.0.0
   triggers:
     - "trigger phrase 1"
     - "trigger phrase 2"
   dependencies:
     - google-workspace  # if needed
   ---
   
   # Skill Instructions
   
   When the user says [trigger phrase], follow these steps:
   
   1. [First step]
   2. [Second step]
   3. [Third step]
   ```

3. **Create learnings_template.md**:
   ```markdown
   # Learnings - My New Skill
   
   This file stores learnings from user feedback.
   
   ## Section Name
   _(No learnings yet)_
   ```

4. **Create README.md** (use this file as template)

### Validating a Skill

```bash
# Quick validation during development
python ~/.claude/skills/skill-creator/scripts/quick_validate.py ~/.claude/skills/my-new-skill/

# Output:
# ✅ SKILL.md exists
# ✅ YAML frontmatter valid
# ✅ references/ directory exists
# ✅ learnings_template.md exists
# ✅ README.md exists
# ⚠️  Warning: No trigger phrases defined
```

### Packaging a Skill

```bash
# Package skill for distribution
python ~/.claude/skills/skill-creator/scripts/package_skill.py ~/.claude/skills/my-new-skill/

# Creates:
# my-new-skill-v1.0.0.zip
# - Includes all files
# - Excludes user-specific learnings.md
# - Includes learnings_template.md
# - Ready for sharing
```

### Example Conversation

```
User: "Help me create a skill that generates meeting agendas"

Claude: I'll guide you through creating a meeting agenda generator skill. Let's start with the key questions:

1. What information does the user need to provide?
   - Meeting type, participants, duration, topics?

2. What should the skill output?
   - Google Doc, email, or both?

3. Should it learn from feedback?
   - Yes (recommended) - include learnings_template.md

4. Any MCP integrations needed?
   - google-workspace for creating Docs
   - gmail for sending emails

Let me create the skill structure for you...

[Creates skill using init_skill.py]
[Generates SKILL.md template]
[Creates README.md]
[Sets up learnings_template.md]

I've created the skill structure at ~/.claude/skills/meeting-agenda-generator/

Next steps:
1. Review SKILL.md and customize the workflow
2. Test the skill in conversation
3. Add learnings as you use it
4. Run validation before sharing

Would you like me to help you customize SKILL.md?

User: "Yes, help me write the SKILL.md"

Claude: I'll create the SKILL.md with a workflow for meeting agendas...

[Writes complete SKILL.md following best practices]
[Includes YAML frontmatter, instructions, examples]

Done! Your skill is ready to test. Try saying:
"Create meeting agenda for product planning meeting"

[User tests and provides feedback]

User: "It works! Now I want to validate and package it"

Claude: Great! Let's validate and package your skill.

[Runs quick_validate.py]
✅ All validation checks passed

[Runs package_skill.py]
✅ Created meeting-agenda-generator-v1.0.0.zip

Your skill is ready to share! You can:
1. Share the .zip file directly
2. Create a GitHub repo for it
3. Contribute it to uxr_plugins via pull request
```

## Skill Structure Requirements

### Required Files

```
skill-name/
├── SKILL.md                    # REQUIRED
├── README.md                   # REQUIRED
└── references/
    └── learnings_template.md   # REQUIRED
```

### Optional Files

```
skill-name/
├── scripts/                    # Python helpers
├── assets/                     # Templates and resources
├── examples/                   # Usage examples
└── LICENSE.txt                 # If different from plugin license
```

### SKILL.md Requirements

**YAML Frontmatter** (required):
```yaml
---
name: skill-name
description: One-line description
version: 1.0.0
triggers:
  - "trigger phrase 1"
  - "trigger phrase 2"
dependencies:
  - google-workspace
  - zen
---
```

**Instructions** (required):
- Clear, step-by-step workflow
- What to do when triggered
- How to handle errors
- When to ask for user input

**Best Practices**:
- Use imperative mood ("Create doc", not "Creates doc")
- Include conditional logic for different scenarios
- Reference learnings.md at start of workflow
- Specify MCP tools to use

### learnings_template.md Requirements

**Format**:
```markdown
# Learnings - Skill Name

This file stores learnings from user feedback.

## Format
Each learning should include:
- The learning/guideline learned
- Context: Which project/section it came from
- Date learned

## Section Name
- Example learning 1 (learned from: Project X, YYYY-MM-DD)
- Example learning 2 (learned from: Project Y, YYYY-MM-DD)

## Another Section
_(No learnings yet)_
```

**Purpose**:
- Provides structure for future learnings
- Shows example format
- Documents learning system for users

## Validation Tools

### quick_validate.py

**Purpose**: Fast validation during development

**Checks**:
- ✅ SKILL.md exists and has content
- ✅ YAML frontmatter is valid
- ✅ Required fields present (name, description, version)
- ✅ references/ directory exists
- ✅ learnings_template.md exists
- ✅ README.md exists (recommended)
- ⚠️ Warnings for missing optional elements

**Usage**:
```bash
python quick_validate.py /path/to/skill/
```

**Exit codes**:
- 0: All checks passed
- 1: Validation errors found

### package_skill.py

**Purpose**: Package skill for distribution

**Features**:
- Creates versioned .zip file
- Excludes user-specific learnings.md
- Includes learnings_template.md
- Validates before packaging
- Generates checksums

**Usage**:
```bash
python package_skill.py /path/to/skill/ [--output /path/to/output/]
```

**Output**:
```
skill-name-v1.0.0.zip
skill-name-v1.0.0.sha256
```

### init_skill.py

**Purpose**: Generate new skill from template

**Features**:
- Creates directory structure
- Generates SKILL.md template
- Creates README.md template
- Initializes learnings_template.md
- Sets up .gitignore (if needed)

**Usage**:
```bash
python init_skill.py skill-name [--template standard|minimal]
```

**Templates**:
- `standard`: Full structure with examples
- `minimal`: Bare minimum required files

## Best Practices

### Skill Design

1. **Clear Triggers**: Use descriptive trigger phrases
   - ✅ "Create survey questionnaire for [topic]"
   - ❌ "Survey" (too vague)

2. **Progressive Disclosure**: Load context incrementally
   - Frontmatter → Core instructions → References → Learnings

3. **Learning Integration**: Always include learnings.md reading
   - Read at start of workflow
   - Apply patterns automatically

4. **Error Handling**: Plan for failure cases
   - MCP connection issues
   - Missing required information
   - Invalid user input

5. **User Feedback Loop**: Build in review steps
   - Create artifact → Share link → Get feedback → Iterate

### Documentation

1. **README.md**: Comprehensive user guide
   - Overview, features, installation
   - Usage examples, troubleshooting
   - Technical details, contributing

2. **SKILL.md**: Clear instructions for Claude
   - Step-by-step workflow
   - Conditional logic
   - Examples and edge cases

3. **learnings_template.md**: Learning format examples
   - Show structure
   - Provide examples
   - Explain purpose

### Testing

1. **Manual Testing**: Test trigger phrases
2. **MCP Integration**: Verify MCP tool usage
3. **Learning System**: Test LEARN keyword extraction
4. **Error Cases**: Test with missing information
5. **Validation**: Run quick_validate.py

## Examples

See existing skills for reference implementations:

- **study-planner**: Complex multi-LLM workflow, extensive learnings
- **interview-guide-writer**: Template integration, best practices
- **feedback-learner**: Advanced logic, LLM integration
- **skill-creator**: Meta-skill (this skill)

## Troubleshooting

### Common Issues

**Issue**: "YAML frontmatter validation failed"
- **Solution**: Check YAML syntax (indentation, hyphens, colons)
- **Tool**: Use online YAML validator

**Issue**: "Skill doesn't activate on trigger phrase"
- **Solution**: Verify trigger phrases in frontmatter
- **Check**: Ensure Claude Code reloaded skills (restart if needed)

**Issue**: "learnings.md not found"
- **Solution**: Create learnings_template.md, not learnings.md
- **Note**: learnings.md is user-specific (not shared)

**Issue**: "Package validation failed"
- **Solution**: Run quick_validate.py first to identify issues
- **Fix**: Address validation errors before packaging

### Getting Help

- **Documentation**: [docs/TROUBLESHOOTING.md](../../docs/TROUBLESHOOTING.md)
- **Issues**: [GitHub Issues](https://github.com/MulanLLL/uxr_plugins/issues)
- **Discussions**: [GitHub Discussions](https://github.com/MulanLLL/uxr_plugins/discussions)

## Technical Details

### File Structure

```
skill-creator/
├── SKILL.md                    # 209 lines - Skill definition
├── README.md                   # This file
├── references/
│   └── learnings_template.md   # Learning format examples
├── scripts/
│   ├── init_skill.py          # Skill template generator
│   ├── package_skill.py        # Skill packager
│   └── quick_validate.py       # Validation tool
└── LICENSE.txt                 # Apache 2.0 (for utilities)
```

### Python Utilities Architecture

**init_skill.py**:
- Argparse for CLI
- Template rendering
- Directory creation
- File generation

**quick_validate.py**:
- YAML parsing
- File existence checks
- Structure validation
- Warning/error reporting

**package_skill.py**:
- Zip creation
- File filtering (.gitignore respect)
- Checksum generation
- Version extraction

## Version History

- **v1.0.0** (2026-01-03): Initial release with 3 validation utilities

## Contributing

We welcome contributions! Ways to help:

- **Add templates**: Create templates for common skill types
- **Improve utilities**: Enhance validation or packaging tools
- **Write guides**: Create tutorials for skill development
- **Share examples**: Contribute reference implementations

See [CONTRIBUTING.md](../../CONTRIBUTING.md) for guidelines.

## License

Apache License 2.0 - See [LICENSE](../../LICENSE) for details.

Python utilities also licensed under Apache 2.0 - See [scripts/LICENSE.txt](scripts/LICENSE.txt).

---

**Part of the UXR Workflow Skills plugin** | [Main Documentation](../../README.md)
