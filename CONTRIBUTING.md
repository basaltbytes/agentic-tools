# Contributing to Basaltbytes Agentic Tools

Thank you for your interest in contributing to our collection of agentic tools! This guide will help you add new tools or extend existing ones to support additional platforms.

## Table of Contents

- [Philosophy](#philosophy)
- [Repository Structure](#repository-structure)
- [Adding a New Tool](#adding-a-new-tool)
- [Adding Platform Support](#adding-platform-support)
- [Documentation Standards](#documentation-standards)
- [Testing Requirements](#testing-requirements)
- [Submission Process](#submission-process)

## Philosophy

This repository is a **platform-agnostic collection of agentic tools** - automated workflows designed to be executed by AI agents across different platforms.

### Key Principles

1. **Platform Agnostic Core**: Each tool is defined conceptually, independent of any platform
2. **Multiple Deployments**: Tools can be deployed to multiple platforms (Claude Code, Cursor, Windsurf, etc.)
3. **Consistent Quality**: All tools should be well-documented, tested, and maintainable
4. **User-Focused**: Tools should solve real development problems effectively

## Repository Structure

```
agentic-tools/
├── tools/                          # Platform-agnostic tool definitions
│   └── {tool-name}/
│       ├── tool.json              # Metadata & platform mappings
│       └── README.md              # Conceptual documentation
│
└── {platform-specific-dir}/       # Platform implementations
    └── {tool-name}/
        └── ...                    # Platform-specific files
```

### Current Platforms

- **Claude Code**: AI-powered code editor plugin system (`.claude-plugin/`)

## Adding a New Tool

### Step 1: Create Platform-Agnostic Definition

Create a new directory in `/tools/{tool-name}/`:

#### `tool.json`

```json
{
  "name": "tool-name",
  "version": "1.0.0",
  "description": "Brief description of what this tool does",
  "author": {
    "name": "Your Name or Organization",
    "email": "contact@example.com"
  },
  "homepage": "https://github.com/basaltbytes/agentic-tools",
  "repository": "https://github.com/basaltbytes/agentic-tools",
  "license": "MIT",
  "keywords": ["relevant", "keywords", "for", "search"],
  "category": "development-automation",
  "platforms": {
    "claude-code": {
      "source": "../../{tool-name}-plugin",
      "commands": ["/command-name"],
      "version": "1.0.0"
    }
  },
  "requirements": {
    "dependencies": ["required-npm-package"],
    "devDependencies": ["required-dev-package"],
    "configFiles": ["required-config-file.json"]
  },
  "workflow": {
    "steps": [
      "Step 1 description",
      "Step 2 description",
      "Step 3 description"
    ]
  }
}
```

#### `README.md`

Platform-agnostic documentation should include:

- **Overview**: What the tool does conceptually
- **What It Does**: Detailed workflow description
- **Requirements**: Dependencies, dev dependencies, config files
- **How It Works**: Step-by-step workflow with diagrams if helpful
- **Usage Patterns**: How AI agents should use this tool
- **Platform Support**: Links to platform-specific implementations
- **Best Practices**: Tips for effective use
- **Limitations**: Known constraints or requirements

### Step 2: Create Platform Implementation

For each platform you want to support, create the platform-specific implementation following that platform's conventions.

#### For Claude Code:

1. Create `/{tool-name}-plugin/` directory
2. Add `.claude-plugin/plugin.json` with metadata
3. Add `commands/{command-name}.md` with AI instructions
4. Add platform-specific `README.md`
5. Update `/.claude-plugin/marketplace.json` to include your tool

See [Claude Code Development Guide](CLAUDE.md) for detailed instructions.

### Step 3: Update Root Documentation

1. Add your tool to the main `README.md` tool catalog
2. Update the platform support matrix
3. Ensure all links work correctly

## Adding Platform Support

To add support for a new platform to an existing tool:

### 1. Create Platform Implementation

Follow the platform's conventions for:
- Directory structure
- Configuration files
- Command definitions
- Documentation format

### 2. Update `tool.json`

Add the new platform to the `platforms` section:

```json
{
  "platforms": {
    "claude-code": { ... },
    "cursor": {
      "source": "../../cursor-plugins/{tool-name}",
      "commands": ["cursor-command"],
      "version": "1.0.0"
    }
  }
}
```

### 3. Link in Platform-Agnostic README

Update `/tools/{tool-name}/README.md` to include installation instructions for the new platform.

## Documentation Standards

### Clarity and Completeness

- Use clear, concise language
- Provide examples where helpful
- Document all requirements and limitations
- Include workflow diagrams for complex tools

### Consistency

- Follow the same structure as existing tools
- Use consistent terminology across all documentation
- Maintain the same tone and style

### Links and References

- All internal links should be relative paths
- External links should be stable and maintained
- Always link to platform-specific docs from tool READMEs

## Testing Requirements

Before submitting:

### Platform-Agnostic Tests

- [ ] `tool.json` is valid JSON
- [ ] All required fields are present
- [ ] Keywords are relevant and searchable
- [ ] README.md is complete and well-formatted

### Platform-Specific Tests

For **Claude Code**:
- [ ] Plugin installs successfully via marketplace
- [ ] Commands execute without errors
- [ ] Documentation is accurate and helpful
- [ ] All file paths in configs are correct

### Integration Tests

- [ ] Tool works on a real project
- [ ] Workflow completes successfully
- [ ] Self-verification loops terminate correctly
- [ ] Error handling works as expected

## Submission Process

### 1. Fork and Branch

```bash
git clone https://github.com/basaltbytes/agentic-tools.git
cd agentic-tools
git checkout -b add-{tool-name}
```

### 2. Develop and Test

- Create tool definition in `/tools/{tool-name}/`
- Create platform implementation(s)
- Test thoroughly on real projects
- Update all documentation

### 3. Submit Pull Request

- Provide clear description of the tool
- List all platforms supported
- Include testing results
- Reference any related issues

### PR Checklist

- [ ] Tool definition created in `/tools/`
- [ ] Platform implementation(s) created
- [ ] All documentation complete
- [ ] Tests passing
- [ ] No duplicate code
- [ ] Follows repository conventions
- [ ] Links work correctly
- [ ] Changelog updated (if applicable)

## Code Quality Guidelines

### Tool Design

- **Single Responsibility**: Each tool should do one thing well
- **Composability**: Tools should work well together
- **Idempotency**: Re-running should be safe
- **Self-Verification**: Include verification steps where possible

### Documentation Quality

- **No Placeholders**: Replace all template text with real content
- **Consistent Formatting**: Use markdown consistently
- **Clear Examples**: Provide concrete usage examples
- **Up-to-Date**: Keep docs synchronized with code

### Metadata Quality

- **Accurate Versions**: Use semantic versioning correctly
- **Relevant Keywords**: Choose searchable, specific keywords
- **Proper Categories**: Use established category names
- **Complete Contact Info**: Provide valid email and homepage

## Platform-Specific Guidelines

### Claude Code

See [CLAUDE.md](CLAUDE.md) for comprehensive Claude Code plugin development guidelines, including:
- Plugin structure requirements
- Command markdown format
- Testing with `claude` CLI
- Marketplace integration

### Future Platforms

As new platforms are added, we'll create dedicated guides:
- `CURSOR.md` - Cursor plugin development
- `WINDSURF.md` - Windsurf integration
- etc.

## Getting Help

- **Issues**: Open an issue on GitHub for questions or problems
- **Discussions**: Use GitHub Discussions for general questions
- **Email**: Contact us at contact@basaltbytes.com

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

## Recognition

Contributors will be acknowledged in:
- Tool metadata (author/contributors field)
- Repository README
- Release notes (for significant contributions)

Thank you for helping build a better collection of agentic development tools!
