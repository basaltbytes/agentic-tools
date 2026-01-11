# i18next Translate Plugin for Claude Code

A Claude Code plugin that automates finding and fixing hardcoded strings in i18next projects with a self-verification loop.

## What it does

The `/translate` command runs an automated workflow:

1. **Detects** your project structure (monolith or monorepo)
2. **Checks status** with `i18next-cli status`
3. **Finds** hardcoded strings with `i18next-cli lint`
4. **Fixes** them by wrapping with `t()` or `<Trans>`
5. **Verifies** the fix worked
6. **Loops** until all strings are translated
7. **Extracts** new keys to your JSON files

## Installation

### From a Marketplace

If this plugin is hosted in a marketplace you've already added:

```
/plugin install i18next-translate@marketplace-name
```

### Direct from GitHub

```
/plugin marketplace add YOUR_USERNAME/i18next-translate-plugin
/plugin install i18next-translate
```

### Local Development

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/i18next-translate-plugin.git

# Test locally
claude --plugin-dir ./i18next-translate-plugin
```

## Usage

### Basic Usage (monolith)

```
/translate
```

### With Path (monorepo)

```
/translate apps/mobile
/translate apps/web
/translate packages/shared
```

### Examples

```
/translate                    # Run in current directory
/translate apps/mobile        # Run in specific app
/translate src                # Run in src folder
```

## Requirements

Your project needs:

- **i18next** and **react-i18next** (or similar binding)
- An `i18next.config.ts` file (run `npx i18next-cli init` to create one)

The plugin auto-detects your package manager (pnpm/yarn/npm) and uses `dlx`/`npx` so i18next-cli doesn't need to be pre-installed.

## Supported Project Structures

### Monolith
```
my-app/
├── i18next.config.ts    ← Config at root
├── src/
└── locales/
```

### Monorepo
```
my-monorepo/
├── apps/
│   ├── web/
│   │   ├── i18next.config.ts
│   │   └── src/
│   └── mobile/
│       ├── i18next.config.ts
│       └── src/
└── packages/
```

## The Self-Verification Loop

```
┌─────────────────────────────────────┐
│         i18next-cli status          │  ← Check progress
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│          i18next-cli lint           │  ← Find hardcoded strings
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│      Fix strings with t()/<Trans>   │  ← Apply fixes
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│         i18next-cli status          │  ← Verify improvement
└──────────────┬──────────────────────┘
               │
         More issues?
         ├── Yes → Loop back to lint
         └── No  → Extract & Done
```

## License

MIT
