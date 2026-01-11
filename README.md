# BasaltBytes Agentic Tools

Professional development tools and plugins for Claude Code by BasaltBytes.

## Installation

Add this marketplace to your Claude Code:

```bash
/plugin marketplace add basaltbytes/agentic-tools
```

Then install any plugin from the marketplace:

```bash
/plugin install i18next-translate
```

## Available Plugins

### [i18next-translate](./i18next-translate-plugin)

Automates finding and fixing hardcoded strings in i18next projects with a self-verification loop.

**Command:** `/translate`

**Features:**
- Detects monolith or monorepo project structure
- Finds hardcoded strings with `i18next-cli lint`
- Fixes them by wrapping with `t()` or `<Trans>`
- Self-verifies until all strings are translated
- Extracts new keys to your JSON files

[View detailed documentation →](./i18next-translate-plugin/README.md)

## Adding More Plugins

This marketplace is designed to host multiple plugins. Each plugin should:

1. Be in its own directory at the root level
2. Contain a `.claude-plugin/plugin.json` file
3. Have a `commands/` directory with command markdown files
4. Include its own README.md

## For Plugin Developers

To add a new plugin to this marketplace:

1. Create a new directory for your plugin
2. Set up the plugin structure:
   ```
   your-plugin/
   ├── .claude-plugin/
   │   └── plugin.json
   ├── commands/
   │   └── yourcommand.md
   └── README.md
   ```
3. Add the plugin entry to `marketplace.json`

See [DISTRIBUTION_GUIDE.md](./DISTRIBUTION_GUIDE.md) for more details.

## License

MIT
