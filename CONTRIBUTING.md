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
├── .claude-plugin/                # Claude Code marketplace
│   └── marketplace.json
│
└── {tool-name}-plugin/            # Tool implementations
    ├── .claude-plugin/
    │   └── plugin.json
    ├── commands/
    │   └── {command}.md
    └── README.md
```

### Current Platforms

- **Claude Code**: Primary platform (marketplace/plugin system)

## Adding a New Tool

For Claude Code (currently our primary platform):

### Step 1: Create Plugin Directory

1. Create `/{tool-name}-plugin/` directory
2. Add `.claude-plugin/plugin.json` with metadata
3. Add `commands/{command-name}.md` with AI instructions
4. Add `README.md` with tool documentation

See [CLAUDE.md](CLAUDE.md) for detailed file structure and examples.

### Step 2: Update Marketplace Configuration

Add your tool entry to `.claude-plugin/marketplace.json`.

### Step 3: Update Root Documentation

1. Add your tool to the main `README.md` tool catalog
2. Update the "Available Tools" section
3. Ensure all links work correctly

## Adding Platform Support

To add support for a tool on a new platform (e.g., Cursor):

1. Create platform-specific implementation directory
2. Follow that platform's conventions for structure and commands
3. Update tool documentation to note multi-platform support
4. Update root `README.md` platform support matrix

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

- Create plugin directory and implementation
- Test thoroughly on real projects
- Update all documentation

### 3. Submit Pull Request

- Provide clear description of the tool
- List all platforms supported
- Include testing results
- Reference any related issues

### PR Checklist

- [ ] Plugin directory created with all required files
- [ ] All documentation complete
- [ ] Tests passing
- [ ] No duplicate code
- [ ] Follows repository conventions
- [ ] Links work correctly
- [ ] Marketplace configuration updated

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
