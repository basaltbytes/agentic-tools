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

**Learn more:** [Tool Documentation →](./tools/i18next-translate)

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
| [i18next-translate](./tools/i18next-translate) | Development Automation | 1.0.0 | Claude Code | Automated i18next string externalization with self-verification |

## For Contributors

### Adding a New Tool

We welcome contributions of new agentic tools! See our [Contributing Guide](./CONTRIBUTING.md) for detailed instructions on:

- Creating platform-agnostic tool definitions
- Implementing platform-specific versions
- Documentation standards
- Testing requirements

### Adding Platform Support

To add support for an existing tool on a new platform:

1. Review the tool's platform-agnostic definition in `/tools/{tool-name}/`
2. Create a platform-specific implementation following that platform's conventions
3. Update the tool's `tool.json` to include the new platform
4. Submit a pull request with your implementation

See [CONTRIBUTING.md](./CONTRIBUTING.md) for details.

## Repository Structure

```
agentic-tools/
├── tools/                          # Platform-agnostic tool definitions
│   └── {tool-name}/
│       ├── tool.json              # Metadata, requirements, platform mappings
│       └── README.md              # Conceptual documentation
│
├── .claude-plugin/                # Claude Code marketplace configuration
│   └── marketplace.json
│
├── {tool-name}-plugin/            # Claude Code implementations
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── commands/
│   │   └── {command}.md
│   └── README.md
│
├── README.md                      # This file
├── CONTRIBUTING.md                # Contribution guidelines
├── CLAUDE.md                      # Claude Code development guide
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
