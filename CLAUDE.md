# Basaltbytes Agentic Tools - Project Context for AI Assistants

## Project Overview

This repository is a **collection of agentic tools** - AI-powered development automation workflows that can be deployed across multiple platforms. Currently supports Claude Code as the primary deployment target, with architecture designed for multi-platform expansion.

**Repository**: `basaltbytes/agentic-tools`
**Organization**: Basaltbytes
**Contact**: contact@basaltbytes.com

## Repository Philosophy

**Multi-Platform Ready**: Tools are designed to be platform-agnostic in concept, with implementations for specific platforms. Currently focused on Claude Code, with architecture that can support future platforms.

**Current Deployment Targets**:
- Claude Code (via marketplace/plugin system)
- Future: Cursor, Windsurf, custom CLIs, etc.

## Repository Structure

```
agentic-tools/
├── .claude-plugin/                # Claude Code marketplace configuration
│   └── marketplace.json           # Lists all available Claude Code plugins
│
├── {tool-name}-plugin/            # Claude Code implementation of a tool
│   ├── .claude-plugin/
│   │   └── plugin.json           # Claude Code plugin manifest
│   ├── commands/
│   │   └── {command}.md          # Command definitions with frontmatter
│   └── README.md                 # Tool documentation
│
├── README.md                      # User-facing repository overview
├── CONTRIBUTING.md                # Contribution guidelines
├── CLAUDE.md                      # This file - context for AI assistants
└── LICENSE                        # MIT license
```

## Current Tools

### i18next-translate
- **Location**: `./i18next-translate-plugin/`
- **Command**: `/translate`
- **Purpose**: Automates finding and fixing hardcoded strings in i18next projects with self-verification loop
- **Category**: development-automation

## How Claude Code Marketplace Works

### Installation by Users

1. Users add the marketplace once:
   ```bash
   /plugin marketplace add basaltbytes/agentic-tools
   ```

2. They can then install any tool as a plugin:
   ```bash
   /plugin install i18next-translate
   ```

3. Use the tool commands:
   ```bash
   /translate
   ```

### Marketplace Structure for Claude Code

- **`.claude-plugin/marketplace.json`**: Declares all Claude Code plugins and their sources
- **Plugin directories**: Each Claude Code plugin is in its own `{name}-plugin/` directory
- **No nested marketplaces**: Plugins should NOT have their own `marketplace.json` files

## Adding a New Tool

When creating a new tool for Claude Code:

### Step 1: Create Plugin Directory Structure

Create `/{tool-name}-plugin/` directory:

#### Directory Structure

```bash
mkdir {tool-name}-plugin
cd {tool-name}-plugin
mkdir -p .claude-plugin commands
```

#### `.claude-plugin/plugin.json`

```json
{
  "name": "tool-name",
  "version": "1.0.0",
  "description": "Clear, concise description",
  "author": {
    "name": "Basaltbytes",
    "email": "contact@basaltbytes.com"
  },
  "homepage": "https://github.com/basaltbytes/agentic-tools",
  "repository": "https://github.com/basaltbytes/agentic-tools",
  "license": "MIT",
  "keywords": ["relevant", "keywords"]
}
```

#### `commands/{command-name}.md`

Command file with frontmatter:

```markdown
---
description: Brief description of what this command does (shown in help)
---

# Command Instructions for Claude

Detailed instructions for how to execute this command.

## Context
What this command is for and when to use it.

## Steps
1. First step
2. Second step

## Important Notes
- Critical considerations
- Error handling
```

#### `README.md`

Tool documentation:

```markdown
# {tool-name}

An agentic tool for Claude Code that [description].

## What it does
[Detailed explanation]

## Installation
[Installation instructions]

## Usage
[Usage examples]
```

### Step 2: Update Marketplace Configuration

Add entry to `.claude-plugin/marketplace.json`:

```json
{
  "name": "tool-name",
  "source": "./{tool-name}-plugin",
  "description": "Brief description for marketplace listing",
  "version": "1.0.0",
  "keywords": ["relevant", "keywords"],
  "category": "development-automation"
}
```

### Step 3: Update Root README

Add the new tool to the "Available Tools" section and tool catalog table in `README.md`.

## Important Conventions

### File Structure Rules

1. **Claude Code plugins**: Always in `/{tool-name}-plugin/` at root level
2. **Single marketplace.json**: Only in `.claude-plugin/marketplace.json` (not at root, not in plugin dirs)
3. **Commands directory**: Always `commands/` (plural) inside each plugin
4. **Command files**: Named `{command-name}.md` matching the command slug

### Metadata Consistency

1. **Organization**: Always use "Basaltbytes" as author name
2. **Email**: Always use "contact@basaltbytes.com"
3. **Repository**: Always point to "https://github.com/basaltbytes/agentic-tools"
4. **License**: MIT for all tools

### Versioning

- Follow semantic versioning (MAJOR.MINOR.PATCH)
- Update version in BOTH `{tool}-plugin/.claude-plugin/plugin.json` AND `.claude-plugin/marketplace.json` entry
- Update marketplace metadata version when adding/removing tools

### Command Frontmatter

Every command markdown file MUST have frontmatter:

```markdown
---
description: Brief description (required)
---
```

## Testing

### Test Claude Code Plugin

```bash
# From plugin directory
claude --plugin-dir .

# Or from repo root
claude --plugin-dir ./{tool-name}-plugin
```

### Test Entire Marketplace

```bash
# From repo root
claude --marketplace-dir .
```

### Validate Plugin Structure

```bash
claude plugin validate ./{tool-name}-plugin
```

## Common Tasks

### Adding Support for a New Platform (e.g., Cursor)

1. Create platform-specific implementation directory (e.g., `{tool-name}-cursor/`)
2. Follow that platform's conventions for structure and commands
3. Update tool documentation to note multi-platform support
4. Update root `README.md` platform support matrix

### Updating a Tool

1. Make changes to tool files
2. Update version in:
   - `{tool-name}-plugin/.claude-plugin/plugin.json`
   - `.claude-plugin/marketplace.json` entry
3. Update relevant README files
4. Test locally
5. Commit and push

### Removing a Tool

1. Remove plugin directory (e.g., `{tool-name}-plugin/`)
2. Remove entry from `.claude-plugin/marketplace.json`
3. Remove from root `README.md`
4. Update marketplace version number
5. Commit and push

## Development Guidelines

### When Working on Tools

1. **Test before committing**: Always test tools locally
2. **Keep tools focused**: Each tool should do one thing well
3. **Document thoroughly**: READMEs should be comprehensive
4. **Follow existing patterns**: Match the style of existing tools
5. **Maintain platform separation**: Keep platform-agnostic and platform-specific code separate

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

## Key Messaging

**This is NOT**: A Claude Code marketplace (though it includes one)
**This IS**: A collection of agentic tools with multi-platform support

Terminology:
- "Tools" (not "plugins") for platform-agnostic references
- "Plugin" only when specifically referring to Claude Code implementation
- "Agentic tools" or "AI-powered automation workflows" for general description

## File Checklist

When adding a new tool, ensure:

- [ ] Claude Code plugin directory created at `/{tool-name}-plugin/`
- [ ] `{tool-name}-plugin/.claude-plugin/plugin.json` exists with correct metadata
- [ ] Command markdown files in `{tool-name}-plugin/commands/` with frontmatter
- [ ] Plugin `README.md` created and complete
- [ ] Entry added to `.claude-plugin/marketplace.json`
- [ ] Root `README.md` updated with new tool
- [ ] All placeholders replaced with actual values
- [ ] Tested locally
- [ ] Version numbers consistent across all files

## Publishing

When ready to publish changes:

```bash
git add .
git commit -m "Add {tool-name} tool" # or "Update {tool-name} v1.2.3"
git push origin main
```

Users will be able to install the new/updated tool immediately after the push.

## Support and Maintenance

- Issues and pull requests are welcome
- Keep tools maintained and up-to-date
- Respond to user feedback
- Update documentation as needed

## Resources

- [Main README](./README.md) - User-facing overview
- [CONTRIBUTING.md](./CONTRIBUTING.md) - Contribution guidelines
- [Claude Code Documentation](https://docs.anthropic.com/claude/docs)
