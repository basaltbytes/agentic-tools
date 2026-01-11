# Claude Code Platform - Development Guide

> **Platform-Specific Documentation**
>
> This guide is specific to developing and deploying tools for the Claude Code platform.
> For general information about this repository and platform-agnostic tool documentation, see the [main README](./README.md).
> For contribution guidelines applicable to all platforms, see [CONTRIBUTING.md](./CONTRIBUTING.md).

## Project Overview

This repository is a **collection of agentic tools** with support for multiple AI-powered development platforms. This document focuses on the **Claude Code implementation**, which provides these tools as plugins via a Claude Code marketplace.

**Repository**: `basaltbytes/agentic-tools`
**Organization**: Basaltbytes
**Contact**: contact@basaltbytes.com

## Claude Code Marketplace

For Claude Code, this repository functions as a **multi-plugin marketplace** that allows users to install multiple development tools from a single marketplace source.

## Repository Structure

```
agentic-tools/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace manifest - lists all available plugins
├── README.md                     # User-facing marketplace overview
├── CLAUDE.md                     # This file - project context for Claude
└── <plugin-name>/                # Each plugin in its own directory
    ├── .claude-plugin/
    │   └── plugin.json          # Plugin manifest (name, version, author, etc.)
    ├── commands/
    │   └── <command>.md         # Command definitions with frontmatter
    └── README.md                 # Plugin-specific documentation
```

## Current Plugins

### i18next-translate
- **Location**: `./i18next-translate-plugin/`
- **Command**: `/translate`
- **Purpose**: Automates finding and fixing hardcoded strings in i18next projects
- **Category**: internationalization

## How This Marketplace Works

### Installation by Users

1. Users add the marketplace once:
   ```bash
   /plugin marketplace add basaltbytes/agentic-tools
   ```

2. They can then install any plugin:
   ```bash
   /plugin install i18next-translate
   ```

3. Use the plugin commands:
   ```bash
   /translate
   ```

### Marketplace Structure

- **Root `.claude-plugin/marketplace.json`**: Declares all plugins and their sources
- **Plugin directories**: Each plugin is self-contained with its own configuration
- **No nested marketplaces**: Plugins should NOT have their own `marketplace.json` files

## Adding a New Plugin

When creating a new plugin for this marketplace:

### 1. Create Plugin Directory Structure

```bash
mkdir <plugin-name>
cd <plugin-name>
mkdir -p .claude-plugin commands
```

### 2. Create `.claude-plugin/plugin.json`

```json
{
  "name": "plugin-name",
  "version": "1.0.0",
  "description": "Clear, concise description of what this plugin does",
  "author": {
    "name": "Basaltbytes",
    "email": "contact@basaltbytes.com"
  },
  "homepage": "https://github.com/basaltbytes/agentic-tools",
  "repository": "https://github.com/basaltbytes/agentic-tools",
  "license": "MIT",
  "keywords": ["relevant", "keywords", "for", "search"]
}
```

### 3. Create Command Files

Each command gets a markdown file in `commands/`:

**File**: `commands/<command-name>.md`

```markdown
---
description: Brief description of what this command does (shown in help)
---

# Command Instructions

Detailed instructions for Claude on how to execute this command.

## Context

Explain what this command is for and when to use it.

## Steps

1. First step
2. Second step
3. Etc.

## Important Notes

- Any critical considerations
- Error handling
- Dependencies required
```

### 4. Update Root `.claude-plugin/marketplace.json`

Add your plugin to the `plugins` array in `.claude-plugin/marketplace.json`:

```json
{
  "name": "plugin-name",
  "source": "./plugin-name",
  "description": "Brief description for marketplace listing",
  "version": "1.0.0",
  "keywords": ["relevant", "keywords"],
  "category": "category-name"
}
```

**Valid categories**:
- development
- testing
- internationalization
- documentation
- productivity
- utilities

### 5. Create Plugin README

Document the plugin in `<plugin-name>/README.md`:

- What it does
- How to install
- How to use
- Requirements
- Examples

### 6. Update Root README

Add the new plugin to the "Available Plugins" section in the root `README.md`

### 7. Version Management

Update the marketplace version in `.claude-plugin/marketplace.json` if needed

## Important Conventions

### File Structure Rules

1. **Marketplace manifest**: Always at root `.claude-plugin/marketplace.json`
2. **Plugin manifest location**: Always at `<plugin-name>/.claude-plugin/plugin.json`
3. **No marketplace.json in plugins**: Only the root `.claude-plugin/` has `marketplace.json`
4. **Commands directory**: Always `commands/` (plural) inside each plugin
5. **Command files**: Named `<command-name>.md` matching the command slug

### Metadata Consistency

1. **Organization**: Always use "Basaltbytes" as author name
2. **Email**: Always use "contact@basaltbytes.com"
3. **Repository**: Always point to "https://github.com/basaltbytes/agentic-tools"
4. **License**: MIT for all plugins

### Versioning

- Follow semantic versioning (MAJOR.MINOR.PATCH)
- Update version in BOTH `<plugin>/.claude-plugin/plugin.json` AND `.claude-plugin/marketplace.json` entry
- Update marketplace metadata version when adding/removing plugins
- Document changes in plugin README

### Command Frontmatter

Every command markdown file MUST have frontmatter:

```markdown
---
description: Brief description (required)
---
```

The description shows up in Claude Code's help system.

## Testing

### Test Individual Plugin

```bash
# From plugin directory
claude --plugin-dir .

# Or from repo root
claude --plugin-dir ./i18next-translate-plugin
```

### Test Entire Marketplace

```bash
# From repo root
claude --marketplace-dir .
```

### Validate Plugin Structure

```bash
claude plugin validate ./plugin-name
```

## Common Tasks

### Updating a Plugin

1. Make changes to plugin files
2. Update version in `<plugin>/.claude-plugin/plugin.json`
3. Update version in root `.claude-plugin/marketplace.json` entry
4. Update plugin README with changes
5. Test locally
6. Commit and push

### Removing a Plugin

1. Remove plugin directory
2. Remove entry from `.claude-plugin/marketplace.json`
3. Remove from root README
4. Update marketplace version number
5. Commit and push

## Development Guidelines

### When Working on Plugins

1. **Test before committing**: Always test plugins locally
2. **Keep plugins focused**: Each plugin should do one thing well
3. **Document thoroughly**: READMEs should be comprehensive
4. **Use clear command names**: Commands should be intuitive
5. **Follow existing patterns**: Match the style of existing plugins

### Command Design

1. **Keep commands simple**: Each command should have a clear purpose
2. **Use arguments wisely**: Optional paths/parameters are fine
3. **Provide good feedback**: Commands should explain what they're doing
4. **Handle errors gracefully**: Include error handling instructions

### Code Quality

1. **No placeholder text**: Replace all "YOUR_USERNAME", "your-email@example.com", etc.
2. **Consistent formatting**: Use consistent markdown and JSON formatting
3. **Clear descriptions**: Avoid jargon, be specific
4. **Test all scenarios**: Consider edge cases

## File Checklist

When adding a new plugin, ensure:

- [ ] Plugin directory created at root level
- [ ] `<plugin>/.claude-plugin/plugin.json` exists with correct metadata
- [ ] Command markdown files in `<plugin>/commands/` with frontmatter
- [ ] Plugin `README.md` created and complete
- [ ] Entry added to `.claude-plugin/marketplace.json`
- [ ] Root `README.md` updated with new plugin
- [ ] No `marketplace.json` inside plugin directory
- [ ] All placeholders replaced with actual values
- [ ] Tested locally with `claude --plugin-dir ./plugin-name`
- [ ] Version numbers match in both files

## Publishing

When ready to publish changes:

```bash
git add .
git commit -m "Add <plugin-name> plugin" # or "Update <plugin-name> v1.2.3"
git push origin main
```

Users will be able to install the new/updated plugin immediately after the push.

## Support and Maintenance

- Issues and pull requests are welcome
- Keep plugins maintained and up-to-date
- Respond to user feedback
- Update documentation as needed

## Resources

- [Claude Code Documentation](https://docs.anthropic.com/claude/docs)
- [Plugin Development Guide](./DISTRIBUTION_GUIDE.md)
- [Claude Code Plugin Examples](https://github.com/anthropics/claude-plugins-official)
