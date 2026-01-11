# Basaltbytes Agentic Tools - Project Context for AI Assistants

## Project Overview

This repository is a **collection of agentic tools** - AI-powered development automation workflows that can be deployed across multiple platforms. Currently supports Claude Code as the primary deployment target, with architecture designed for multi-platform expansion.

**Repository**: `basaltbytes/agentic-tools`
**Organization**: Basaltbytes
**Contact**: contact@basaltbytes.com

## Repository Philosophy

**Platform-Agnostic Core**: Each tool is defined conceptually in `/tools/` directory, independent of any specific platform. Platform-specific implementations live in separate directories (e.g., `i18next-translate-plugin/` for Claude Code).

**Current Deployment Targets**:
- Claude Code (via marketplace/plugin system)
- Future: Cursor, Windsurf, custom CLIs, etc.

## Repository Structure

```
agentic-tools/
├── tools/                          # Platform-agnostic tool definitions (source of truth)
│   └── {tool-name}/
│       ├── tool.json              # Metadata, requirements, platform mappings
│       └── README.md              # Conceptual workflow documentation
│
├── .claude-plugin/                # Claude Code marketplace configuration
│   └── marketplace.json           # Lists all available Claude Code plugins
│
├── {tool-name}-plugin/            # Claude Code implementation of a tool
│   ├── .claude-plugin/
│   │   └── plugin.json           # Claude Code plugin manifest
│   ├── commands/
│   │   └── {command}.md          # Command definitions with frontmatter
│   └── README.md                 # Claude Code-specific usage docs
│
├── README.md                      # User-facing repository overview
├── CONTRIBUTING.md                # Contribution guidelines for all platforms
├── CLAUDE.md                      # This file - context for AI assistants
└── LICENSE                        # MIT license
```

## Current Tools

### i18next-translate
- **Platform-agnostic definition**: `./tools/i18next-translate/`
- **Claude Code implementation**: `./i18next-translate-plugin/`
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

When creating a new tool, you MUST create BOTH the platform-agnostic definition AND at least one platform implementation.

### Step 1: Create Platform-Agnostic Tool Definition

Create in `/tools/{tool-name}/`:

#### `tools/{tool-name}/tool.json`

```json
{
  "name": "tool-name",
  "version": "1.0.0",
  "description": "Clear description of what this tool does",
  "author": {
    "name": "Basaltbytes",
    "email": "contact@basaltbytes.com"
  },
  "homepage": "https://github.com/basaltbytes/agentic-tools",
  "repository": "https://github.com/basaltbytes/agentic-tools",
  "license": "MIT",
  "keywords": ["relevant", "keywords"],
  "category": "development-automation",
  "platforms": {
    "claude-code": {
      "source": "../../{tool-name}-plugin",
      "commands": ["/command-name"],
      "version": "1.0.0"
    }
  },
  "requirements": {
    "dependencies": ["required-packages"],
    "devDependencies": ["dev-packages"],
    "configFiles": ["config-files-needed"]
  },
  "workflow": {
    "steps": [
      "Step 1 description",
      "Step 2 description"
    ]
  }
}
```

#### `tools/{tool-name}/README.md`

Platform-agnostic documentation explaining:
- What the tool does conceptually
- The workflow it automates
- Requirements
- How it works (with diagrams if helpful)
- Platform support matrix
- Links to platform-specific implementations

### Step 2: Create Claude Code Plugin Implementation

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

Add header linking to platform-agnostic docs:

```markdown
# {tool-name} - Claude Code Implementation

> **Platform-Specific Implementation**
>
> This is the Claude Code implementation of the [{tool-name} tool](../tools/{tool-name}).
> For platform-agnostic documentation and conceptual overview, see the [tool README](../tools/{tool-name}/README.md).

[Rest of Claude Code specific documentation]
```

### Step 3: Update Marketplace Configuration

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

### Step 4: Update Root README

Add the new tool to the "Available Tools" section and tool catalog table in `README.md`.

## Important Conventions

### File Structure Rules

1. **Platform-agnostic definitions**: Always in `/tools/{tool-name}/`
2. **Claude Code plugins**: Always in `/{tool-name}-plugin/` at root level
3. **Single marketplace.json**: Only in `.claude-plugin/marketplace.json` (not at root, not in plugin dirs)
4. **Commands directory**: Always `commands/` (plural) inside each plugin
5. **Command files**: Named `{command-name}.md` matching the command slug

### Metadata Consistency

1. **Organization**: Always use "Basaltbytes" as author name
2. **Email**: Always use "contact@basaltbytes.com"
3. **Repository**: Always point to "https://github.com/basaltbytes/agentic-tools"
4. **License**: MIT for all tools

### Versioning

- Follow semantic versioning (MAJOR.MINOR.PATCH)
- Update version in BOTH `tools/{tool}/tool.json` AND `.claude-plugin/marketplace.json` entry
- Update version in `{tool}-plugin/.claude-plugin/plugin.json`
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
3. Update `tools/{tool-name}/tool.json` to add new platform entry
4. Update `tools/{tool-name}/README.md` to document new platform
5. Update root `README.md` platform support matrix

### Updating a Tool

1. Make changes to tool files
2. Update version in:
   - `tools/{tool-name}/tool.json`
   - `{tool-name}-plugin/.claude-plugin/plugin.json`
   - `.claude-plugin/marketplace.json` entry
3. Update relevant README files
4. Test locally
5. Commit and push

### Removing a Tool

1. Remove tool directory from `/tools/`
2. Remove plugin directory (e.g., `{tool-name}-plugin/`)
3. Remove entry from `.claude-plugin/marketplace.json`
4. Remove from root `README.md`
5. Update marketplace version number
6. Commit and push

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

- [ ] Platform-agnostic definition created in `/tools/{tool-name}/`
- [ ] `tools/{tool-name}/tool.json` exists with correct metadata
- [ ] `tools/{tool-name}/README.md` created and complete
- [ ] Claude Code plugin directory created at `/{tool-name}-plugin/`
- [ ] `{tool-name}-plugin/.claude-plugin/plugin.json` exists
- [ ] Command markdown files in `{tool-name}-plugin/commands/` with frontmatter
- [ ] Plugin `README.md` created with platform context header
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
