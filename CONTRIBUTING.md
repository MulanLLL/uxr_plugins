# Contributing to UXR Workflow Skills

Thank you for your interest in contributing to the UXR Workflow Skills plugin! This document provides guidelines for contributing to the project.

## Table of Contents

- [Ways to Contribute](#ways-to-contribute)
- [Getting Started](#getting-started)
- [Pull Request Process](#pull-request-process)
- [Skill Structure Requirements](#skill-structure-requirements)
- [Learning Contribution Format](#learning-contribution-format)
- [Code Standards](#code-standards)
- [Security Requirements](#security-requirements)
- [Testing Guidelines](#testing-guidelines)
- [Review Criteria](#review-criteria)

---

## Ways to Contribute

We welcome contributions in several forms:

### 1. Improve Existing Skills

- **Add learnings**: Share patterns you've discovered through your own usage
- **Fix bugs**: Report and fix issues you encounter
- **Enhance documentation**: Clarify instructions, add examples, fix typos
- **Update references**: Add new best practices to reference materials

### 2. Create New Skills

- Follow the skill structure requirements below
- Create comprehensive documentation
- Include learnings_template.md with examples
- Test thoroughly before submitting

### 3. Improve Documentation

- Add usage examples
- Create tutorials and guides
- Improve installation instructions
- Translate documentation

### 4. Report Issues

- Use GitHub Issues to report bugs
- Provide detailed reproduction steps
- Include your environment details
- Suggest improvements

---

## Getting Started

### Prerequisites

- Git installed
- Claude Code installed ([claude.ai/code](https://claude.ai/code))
- Google Workspace account (for testing MCP integration)
- Python 3.8+ (for skill-creator utilities)

### Fork and Clone

1. Fork the repository on GitHub
2. Clone your fork locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/uxr_plugins.git
   cd uxr_plugins
   ```
3. Add the upstream remote:
   ```bash
   git remote add upstream https://github.com/MulanLLL/uxr_plugins.git
   ```
4. Create a feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```

---

## Pull Request Process

### 1. Make Your Changes

- Make your changes in your feature branch
- Follow the code standards and skill structure requirements
- Test your changes thoroughly
- Update documentation as needed

### 2. Commit Your Changes

Use clear, descriptive commit messages:

```bash
git add .
git commit -m "Add: New feature description"
```

Commit message prefixes:
- `Add:` - New features or files
- `Fix:` - Bug fixes
- `Update:` - Changes to existing features
- `Docs:` - Documentation only changes
- `Refactor:` - Code refactoring
- `Test:` - Adding or updating tests

### 3. Push to Your Fork

```bash
git push origin feature/your-feature-name
```

### 4. Submit Pull Request

1. Go to the original repository on GitHub
2. Click "New Pull Request"
3. Select your fork and feature branch
4. Fill in the PR template:
   - **Title**: Clear, descriptive title
   - **Description**: What changes you made and why
   - **Testing**: How you tested your changes
   - **Screenshots**: If applicable
5. Submit the PR

### 5. Address Review Feedback

- Respond to reviewer comments
- Make requested changes
- Push updates to the same branch (PR updates automatically)

---

## Skill Structure Requirements

All skills must follow this structure:

```
skills/{skill-name}/
├── SKILL.md                    # REQUIRED: Skill definition
├── README.md                   # REQUIRED: User documentation
├── references/                 # REQUIRED: Reference materials
│   └── learnings_template.md   # REQUIRED: Learning examples
├── scripts/                    # Optional: Helper scripts
└── assets/                     # Optional: Templates and resources
```

### SKILL.md Requirements

Must include:

1. **YAML Frontmatter**:
   ```yaml
   ---
   name: skill-name
   description: Brief description
   version: 1.0.0
   triggers:
     - "trigger phrase 1"
     - "trigger phrase 2"
   ---
   ```

2. **Clear Instructions**: Step-by-step workflow for Claude Code

3. **Dependencies**: List all MCP servers and other requirements

4. **Examples**: Show expected inputs and outputs

### README.md Requirements

Must include:

- **Overview**: What the skill does
- **When to Use**: Trigger phrases and use cases
- **Features**: Key capabilities
- **Installation**: How to install
- **Dependencies**: Required MCP servers
- **Usage**: Example conversation flow
- **Configuration**: How to customize
- **Examples**: Detailed examples
- **Troubleshooting**: Common issues

### learnings_template.md Requirements

Must include:

- **Format explanation**: How learnings are structured
- **Examples**: At least 3 example learnings
- **Sections**: Organized by document sections or topics
- **Context**: Include date and project context

Example format:

```markdown
# Learnings - Skill Name

## Section Name
- Learning pattern 1 (learned from: Project X, 2026-01-03)
- Learning pattern 2 (learned from: Project Y, 2026-01-15)

## Another Section
- Learning pattern 3 (learned from: Project Z, 2026-02-01)
```

---

## Learning Contribution Format

When contributing learnings to existing skills:

### Structure

Organize learnings by document section or topic:

```markdown
## Timeline Section
- Include weekly timeline with specific milestones
- Specify start and end dates for each week

## Methodology Section
- Specify exact numbers: "12 interviews" not "user interviews"
- Include duration and format: "45-minute semi-structured interviews"
```

### Best Practices

**Do**:
- ✅ Make learnings generalizable (applicable to multiple projects)
- ✅ Include context (which section, which project, when)
- ✅ Use actionable language ("Include X", "Specify Y")
- ✅ Provide examples of better phrasing

**Don't**:
- ❌ Include project-specific details (company names, specific products)
- ❌ Make learnings too vague ("Be more specific")
- ❌ Duplicate existing learnings
- ❌ Include personal opinions without evidence

### Example Contribution

**Good Learning Contribution**:
```markdown
## Research Questions Section
- Frame questions as specific, answerable inquiries
- Example: "How do users currently solve problem X?" instead of "User needs"
- Include both exploratory and evaluative questions
(learned from: Mobile App Study, 2026-01-20)
```

**Poor Learning Contribution**:
```markdown
## Research Questions
- Make questions better
- Be more specific
```

---

## Code Standards

### Python Code

- Follow PEP 8 style guide
- Use type hints where appropriate
- Include docstrings for functions and classes
- Keep functions small and focused
- Use descriptive variable names

Example:

```python
def extract_learning_from_comment(
    comment: dict,
    document_content: str
) -> Optional[str]:
    """
    Extract a generalizable learning from a comment with context.
    
    Args:
        comment: Comment dict with 'content', 'quotedText', 'anchor'
        document_content: Full document text for context
    
    Returns:
        Generalized learning pattern or None if not applicable
    """
    # Implementation
```

### Markdown Documentation

- Use clear headings hierarchy (# → ## → ###)
- Include code examples in fenced code blocks with language
- Use tables for structured data
- Include links to related documentation
- Break long sections into subsections

### SKILL.md Format

- Start with YAML frontmatter
- Use clear, imperative instructions
- Include conditional logic where needed
- Reference learnings.md at the start

---

## Security Requirements

**Critical**: Never commit sensitive data to the repository.

### What NOT to Commit

- ❌ User-specific learnings.md (only learnings_template.md)
- ❌ API credentials or tokens
- ❌ MCP configuration files (.mcp.json, mcp_config.json)
- ❌ Personal Google account information
- ❌ Project-specific data
- ❌ Email addresses (except in author metadata)

### .gitignore Coverage

Before submitting, verify .gitignore excludes:

```gitignore
skills/*/references/learnings.md
.mcp.json
mcp_config.json
__pycache__/
*.pyc
.env
credentials.json
token.pickle
```

### Security Checklist

Before submitting a PR:

```bash
# Search for potential sensitive data
grep -ri "credentials" .
grep -ri "token" .
grep -ri "secret" .
grep -ri "api.key" .
grep -ri "@gmail.com" . # Except in plugin.json author field
```

All searches should return no results (or only safe occurrences).

---

## Testing Guidelines

### Local Testing

1. **Install Plugin Locally**:
   ```bash
   # Copy to Claude Code skills directory
   cp -r skills/* ~/.claude/skills/
   
   # OR test entire plugin
   /plugin validate /path/to/uxr_plugins
   ```

2. **Test Each Skill**:
   - Trigger the skill in Claude Code conversation
   - Verify it creates expected outputs
   - Test with Google Drive integration
   - Test learning system (add LEARN comments)

3. **Test MCP Dependencies**:
   - Verify Google Workspace MCP is connected
   - Test document creation
   - Test folder creation
   - Test comment reading (for feedback-learner)

### Validation

Run validation checks:

```bash
# Validate plugin structure
/plugin validate .

# Validate individual skills (if skill-creator utilities available)
python skills/skill-creator/scripts/quick_validate.py skills/YOUR_SKILL/
```

### Manual Testing Checklist

- [ ] Skill activates on trigger phrases
- [ ] Creates Google Doc/Form/Drive artifacts correctly
- [ ] Reads learnings_template.md successfully
- [ ] Follows all instructions in SKILL.md
- [ ] Error handling works for edge cases
- [ ] Documentation is clear and accurate
- [ ] Examples in README match actual behavior

---

## Review Criteria

Pull requests are evaluated on:

### 1. Structure

- [ ] Follows skill structure requirements
- [ ] All required files present (SKILL.md, README.md, learnings_template.md)
- [ ] File organization is logical

### 2. Documentation

- [ ] README is clear and comprehensive
- [ ] SKILL.md has clear instructions
- [ ] learnings_template.md has useful examples
- [ ] Code comments where needed

### 3. Testing

- [ ] Changes tested locally
- [ ] No regressions in existing functionality
- [ ] Edge cases considered

### 4. Security

- [ ] No sensitive data committed
- [ ] .gitignore properly configured
- [ ] Credentials handled via MCP only

### 5. Backward Compatibility

- [ ] Doesn't break existing skills
- [ ] learnings.md format maintained
- [ ] Plugin structure unchanged (unless intentional)

### 6. Code Quality

- [ ] Python code follows PEP 8
- [ ] Markdown is well-formatted
- [ ] No unnecessary files

### 7. Learning Quality (if contributing learnings)

- [ ] Generalizable patterns (not project-specific)
- [ ] Actionable and clear
- [ ] Properly categorized by section
- [ ] Includes context and dates

---

## Questions or Issues?

- **Questions**: [GitHub Discussions](https://github.com/MulanLLL/uxr_plugins/discussions)
- **Bugs**: [GitHub Issues](https://github.com/MulanLLL/uxr_plugins/issues)
- **Security**: Email ritachengl@gmail.com directly

---

## Code of Conduct

- Be respectful and professional
- Provide constructive feedback
- Welcome newcomers
- Focus on what's best for the project and users

---

## License

By contributing, you agree that your contributions will be licensed under the Apache License 2.0.

---

Thank you for contributing to UXR Workflow Skills! 🎉
