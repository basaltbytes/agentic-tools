# i18next-translate

Automated i18next hardcoded string detection and translation workflow with self-verification.

## Overview

This agentic tool automates the process of finding and fixing hardcoded strings in i18next projects. It uses a self-verification loop to iteratively identify hardcoded strings, replace them with proper i18next translation calls, and verify the fixes until all strings are properly internationalized.

## What It Does

The tool implements a complete workflow for i18next string externalization:

1. **Detection**: Scans your codebase using i18next-cli to find hardcoded strings
2. **Fixing**: Automatically replaces hardcoded strings with appropriate i18next translation patterns
3. **Verification**: Re-runs the linter to confirm fixes and identify remaining issues
4. **Iteration**: Repeats the process until all hardcoded strings are resolved

## Requirements

### Dependencies

Your project must have:
- `i18next` - The core i18next library
- `react-i18next` (for React projects) - React bindings for i18next

### Dev Dependencies

- `i18next-cli` - Command-line tools for linting and extracting translations

### Configuration Files

One of the following i18next configuration files must exist in your project:
- `i18next.config.ts`
- `i18next.config.js`
- `i18next.config.mjs`

## How It Works

The workflow follows this pattern:

```
┌─────────────────────────────────────────┐
│  Run i18next-cli lint                   │
│  └─> Find hardcoded strings             │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  Analyze lint output                    │
│  └─> Identify files & string locations  │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  Fix hardcoded strings                  │
│  └─> Replace with t() calls             │
│  └─> Add translation keys               │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│  Verify fixes                           │
│  └─> Re-run i18next-cli lint            │
└──────────────┬──────────────────────────┘
               │
               ▼
         All strings fixed?
               │
         No ───┘ (loop back to analyze)
               │
         Yes ──▼ Done!
```

## Usage Patterns

This tool is designed to work with AI agents that can:
- Execute shell commands (to run i18next-cli)
- Read and modify files (to fix hardcoded strings)
- Parse linter output (to identify issues)
- Iterate on tasks (to handle multiple strings)

### Typical Workflow

1. Agent runs `i18next-cli lint` to identify hardcoded strings
2. Agent reads the files containing hardcoded strings
3. Agent replaces hardcoded text with `t('translation.key')` calls
4. Agent adds corresponding translation keys to translation files
5. Agent re-runs lint to verify fixes
6. Agent repeats steps 2-5 until no hardcoded strings remain

## Platform Support

This tool is currently available for:

### Claude Code
- **Installation**: `/plugin marketplace add basaltbytes/agentic-tools` then `/plugin install i18next-translate`
- **Command**: `/translate`
- **Documentation**: See [Claude Code implementation](../../i18next-translate-plugin/README.md)

## Best Practices

### Translation Key Naming

The tool works best when translation keys follow consistent patterns:
- Use descriptive, hierarchical keys: `common.buttons.submit`, not `btn1`
- Group related translations: `errors.validation.required`, `errors.validation.email`
- Match your codebase structure when possible

### Configuration

Ensure your `i18next.config` file is properly set up:
- Specify all source file locations
- Define translation file paths
- Configure linting rules appropriately

### Verification

The self-verification loop ensures:
- All hardcoded strings are found and fixed
- No new hardcoded strings are introduced during fixes
- Translation keys are properly added to translation files

## Limitations

- Only works with projects already using i18next
- Requires i18next-cli to be installed and configured
- Agent must have file read/write permissions
- Best results with well-structured i18next configuration

## Contributing

To add support for additional platforms or improve this tool, see [CONTRIBUTING.md](../../CONTRIBUTING.md).

## License

MIT - See [LICENSE](../../LICENSE)

## Support

- **Repository**: https://github.com/basaltbytes/agentic-tools
- **Issues**: https://github.com/basaltbytes/agentic-tools/issues
- **Contact**: contact@basaltbytes.com
