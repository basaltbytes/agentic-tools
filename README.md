# Basaltbytes Agentic Tools

A collection of agents, skills or plugin for agentic development.

**Organization**: [Basaltbytes](https://github.com/basaltbytes)
**Repository**: [basaltbytes/agentic-tools](https://github.com/basaltbytes/agentic-tools)
**License**: MIT

## Available Tools

### [i18next-translate](./i18next-translate-plugin/README.md)

Automated i18next hardcoded string detection and translation workflow with self-verification.

**Category**: Development Automation
**Version**: 1.0.0

**What it does:**
- Detects monolith or monorepo project structure
- Finds hardcoded strings using `i18next-cli lint`
- Fixes them by wrapping with `t()` or `<Trans>` components
- Self-verifies until all strings are properly internationalized
- Extracts new translation keys to your JSON files

**Platform Support:**
- ✅ **Claude Code** - `/translate` command ([docs](./i18next-translate-plugin/README.md))

## Platform Support

### Claude Code

Our tools are available as plugins for Claude Code via marketplace installation.

**Installation:**

```bash
# Add the Basaltbytes marketplace
/plugin marketplace add basaltbytes/agentic-tools

# Install a specific tool
/plugin install i18next-translate

# Use the tool
/translate
```


### Future Platforms

We're exploring support for additional AI-powered development platforms. If you'd like to see support for a specific platform, please [open an issue](https://github.com/basaltbytes/agentic-tools/issues).

## Tool Catalog

| Tool | Category | Version | Platforms | Description |
|------|----------|---------|-----------|-------------|
| [i18next-translate](./i18next-translate-plugin) | Development Automation | 1.0.0 | Claude Code | Automated i18next string externalization with self-verification |

## For Contributors

We welcome contributions of new agentic tools! See our [Contributing Guide](./CONTRIBUTING.md) for detailed instructions on:

- Creating new tools
- Adding platform support for existing tools
- Documentation standards
- Testing requirements

## Repository Structure

```
agentic-tools/
├── .claude-plugin/                # Claude Code marketplace configuration
│   └── marketplace.json
│
├── {tool-name}-plugin/            # Tool implementations for Claude Code
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── commands/
│   │   └── {command}.md
│   └── README.md
│
├── README.md                      # This file
├── CONTRIBUTING.md                # Contribution guidelines
├── CLAUDE.md                      # Project context for AI assistants
└── LICENSE                        # MIT license
```

## License

MIT License - see [LICENSE](./LICENSE) for details.

## Acknowledgments

Repo owner: [PhilDL](https://github.com/PhilDL).

Special thanks to all contributors who help make AI-assisted development more powerful and accessible.
