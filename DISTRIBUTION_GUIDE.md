# Distribution Guide for i18next-translate Plugin

## Plugin Structure

```
i18next-translate-plugin/
├── .claude-plugin/
│   ├── plugin.json          # Plugin manifest (required)
│   └── marketplace.json     # Optional: if self-hosting marketplace
├── commands/
│   └── translate.md         # The /translate slash command
└── README.md
```

---

## Option 1: Self-Host Your Own Marketplace (Recommended for Control)

This gives you full control and allows users to install directly.

### Step 1: Create GitHub Repository

```bash
# Create and push to GitHub
cd i18next-translate-plugin
git init
git add .
git commit -m "Initial release"
gh repo create i18next-translate-plugin --public --source=. --push
```

### Step 2: Users Install Your Plugin

Users add your marketplace and install:

```
/plugin marketplace add YOUR_USERNAME/i18next-translate-plugin
/plugin install i18next-translate
```

Or in one step from the CLI:

```bash
npx claude-plugins install @YOUR_USERNAME/i18next-translate-plugin/i18next-translate
```

---

## Option 2: Submit to Community Marketplaces

Submit your plugin to existing popular marketplaces for wider reach.

### Anthropic Official Marketplace

The official marketplace for high-quality plugins:

**Repository**: https://github.com/anthropics/claude-plugins-official

**Process**:
1. Fork the repository
2. Add your plugin to `/external_plugins/`
3. Open a Pull Request
4. Wait for review

### Community Marketplaces

**cc-marketplace** (ananddtyagi):
- https://github.com/ananddtyagi/cc-marketplace
- Submit via: https://claudecodecommands.directory/submit

**claude-plugins.dev**:
- https://claude-plugins.dev/
- Community registry with CLI install support

---

## Option 3: NPM Package (For npm-centric Distribution)

Wrap the plugin as an npm package for `npx` installation.

### Step 1: Create package.json

```json
{
  "name": "i18next-translate-plugin",
  "version": "1.0.0",
  "description": "Claude Code plugin for i18next translation workflow",
  "files": [
    ".claude-plugin",
    "commands",
    "README.md"
  ],
  "keywords": [
    "claude-code",
    "plugin",
    "i18next",
    "translation",
    "i18n"
  ],
  "license": "MIT"
}
```

### Step 2: Publish

```bash
npm publish
```

Users then manually copy from node_modules or you provide an install script.

---

## Validation & Testing

### Test Locally Before Publishing

```bash
# Method 1: Use --plugin-dir flag
claude --plugin-dir ./i18next-translate-plugin

# Method 2: Validate the plugin structure
claude plugin validate ./i18next-translate-plugin
```

### Test the Command

Once loaded, test with:

```
/i18next-translate:translate
/i18next-translate:translate apps/mobile
```

(Commands are namespaced with the plugin name)

---

## Quick Checklist

- [ ] `plugin.json` has name, version, description
- [ ] `commands/translate.md` has frontmatter with `description`
- [ ] Update placeholder `YOUR_USERNAME` in plugin.json
- [ ] Test locally with `claude --plugin-dir`
- [ ] Push to GitHub
- [ ] Share the marketplace add command

---

## User Installation Commands

Once published, share these with users:

```bash
# Add your marketplace
/plugin marketplace add YOUR_USERNAME/i18next-translate-plugin

# Install the plugin
/plugin install i18next-translate

# Use it!
/i18next-translate:translate
```

Or the one-liner if they have the CLI helper:

```bash
npx claude-plugins install @YOUR_USERNAME/i18next-translate-plugin/i18next-translate
```
