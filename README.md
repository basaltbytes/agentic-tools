# Basaltbytes Agentic Tools

A collection of AI-powered development automation tools designed for agentic workflows. These tools help AI assistants automate complex, repetitive development tasks with self-verification and iterative improvement.

**Organization**: [Basaltbytes](https://github.com/basaltbytes)
**Repository**: [basaltbytes/agentic-tools](https://github.com/basaltbytes/agentic-tools)
**License**: MIT

## What Are Agentic Tools?

Agentic tools are automated workflows designed to be executed by AI agents. Unlike traditional CLI tools or scripts, these tools:

- **Self-verify**: Include built-in verification loops to ensure quality
- **Iterate**: Continue working until the task is complete
- **Adapt**: Can handle different project structures and configurations
- **Collaborate**: Work with AI assistants to solve complex problems

Each tool is platform-agnostic at its core, with implementations available for various AI-powered development platforms.

## Available Tools

### i18next-translate

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

**Platform Documentation:** [CLAUDE.md](./CLAUDE.md)

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

## Requirements

Each tool has its own requirements, but generally you'll need:

- **Node.js**: Most tools work with Node.js projects
- **Project-specific dependencies**: Tools may require specific libraries (e.g., i18next)
- **AI Platform**: Claude Code or another supported platform

Check individual tool documentation for specific requirements.

## Philosophy

This collection is built on these principles:

1. **Platform Agnostic**: Tools are conceptually independent of any platform
2. **Quality First**: Self-verification ensures reliable results
3. **Developer Focused**: Solve real, practical development problems
4. **Open Source**: MIT licensed, contributions welcome

## Support

- **Issues**: [GitHub Issues](https://github.com/basaltbytes/agentic-tools/issues)
- **Discussions**: [GitHub Discussions](https://github.com/basaltbytes/agentic-tools/discussions)
- **Email**: contact@basaltbytes.com

## Roadmap

### In Development

- Additional i18n tools for other frameworks
- Code quality automation tools
- Testing workflow automation

### Exploring

- Support for Cursor IDE
- Support for Windsurf
- Custom CLI implementations

Want to see something specific? [Let us know!](https://github.com/basaltbytes/agentic-tools/issues)

## License

MIT License - see [LICENSE](./LICENSE) for details.

## Acknowledgments

Built with care by [Basaltbytes](https://github.com/basaltbytes).

Special thanks to all contributors who help make AI-assisted development more powerful and accessible.

---

**Note for Existing Claude Code Users**: If you've already installed tools from this marketplace, nothing changes! All commands and functionality remain the same. We've simply reorganized the documentation to better reflect our multi-platform vision.
