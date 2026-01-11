---
description: Find and fix hardcoded strings using i18next-cli with a self-verification loop
---

# Translation Workflow for i18next

You are running a translation workflow to find and fix hardcoded strings using i18next-cli.

## Arguments

- `$ARGUMENTS` - Optional path to app directory (for monorepos), e.g., `apps/mobile`

## Step 1: Detect Project Structure

First, determine where to run commands:

```bash
# If path provided, cd into it
# Otherwise, check current directory for config
find . -maxdepth 3 -name "i18next.config.ts" -o -name "i18next.config.js" -o -name "i18next.config.mjs" 2>/dev/null | head -10
```

**Determine project type:**
- **Monolith**: Config at project root → work from root
- **Monorepo**: Config in `apps/*` or `packages/*` → cd into that directory

If no config found, ask user if they want to create one with `npx i18next-cli init`.

## Step 2: Detect Package Manager

```bash
# Check lockfiles to determine package manager
if [ -f "pnpm-lock.yaml" ]; then
  echo "pnpm"
elif [ -f "yarn.lock" ]; then
  echo "yarn"
else
  echo "npm"
fi
```

Use the appropriate runner:
- pnpm → `pnpm dlx i18next-cli` or `pnpm i18next-cli` if installed
- yarn → `yarn dlx i18next-cli`
- npm → `npx i18next-cli`

## Step 3: Check Initial Status

Get baseline translation status:

```bash
<package-runner> i18next-cli status
```

Report to user:
- Overall progress per locale (%)
- Number of missing keys
- Which namespaces need attention

## Step 4: Self-Verification Loop

Enter the fix-and-verify loop:

### 4a. LINT - Find Hardcoded Strings

```bash
<package-runner> i18next-cli lint
```

Parse the output to identify:
- File paths with issues
- Line numbers
- The hardcoded text

### 4b. FIX - Apply Translations

For each hardcoded string found, apply the appropriate fix:

**Plain text in JSX:**
```tsx
// ❌ Before
<Text>Welcome back!</Text>

// ✅ After  
<Text>{t('welcome_back')}</Text>
```

**Text with interpolation:**
```tsx
// ❌ Before
<Text>Hello {userName}!</Text>

// ✅ After
<Text>{t('hello_user', { name: userName })}</Text>
```

**Rich text with nested elements (use Trans component):**
```tsx
// ❌ Before
<Text>Read our <Link>terms</Link></Text>

// ✅ After
import { Trans } from 'react-i18next';
<Trans i18nKey="read_terms">
  Read our <Link>terms</Link>
</Trans>
```

**Attributes:**
```tsx
// ❌ Before
<Input placeholder="Enter email" />

// ✅ After
<Input placeholder={t('placeholder_email')} />
```

**Ensure t() is available in the file:**
```tsx
// For React components - add if missing
import { useTranslation } from 'react-i18next';

function MyComponent() {
  const { t } = useTranslation();
  // or with namespace: useTranslation('common')
}
```

### 4c. STATUS - Verify Progress

```bash
<package-runner> i18next-cli status
```

Compare with previous run. If issues remain, continue the loop.

### 4d. Repeat or Exit

- **More hardcoded strings found** → Go back to 4a (LINT)
- **No more issues** → Proceed to Step 5
- **User requests stop** → Proceed to Step 5

## Step 5: Extract Keys

Sync translation files with new keys:

```bash
<package-runner> i18next-cli extract
```

This updates JSON files with any new keys.

## Step 6: Final Report

```bash
<package-runner> i18next-cli status
```

Summarize to user:
- How many files were modified
- How many new keys were added
- Current translation progress
- Any remaining work needed

## CLI Quick Reference

| Command | Purpose |
|---------|---------|
| `i18next-cli status` | Translation progress overview |
| `i18next-cli status de` | Detailed report for German locale |
| `i18next-cli lint` | Find hardcoded strings |
| `i18next-cli extract` | Extract keys to JSON |
| `i18next-cli init` | Create config interactively |
