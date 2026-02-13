# code-simplifier-tldr

Claude Code plugin that simplifies code using TLDR-aware AST summaries. Reads structure first via lightweight summaries, then targets only the files that need changes. Saves 80%+ tokens compared to reading every file fully.

When paired with [mercator-ai](https://github.com/shihwesley/mercator-ai), it uses the merkle manifest for O(1) change detection — only looking at files that actually changed.

## Install

```bash
# From the shihwesley-plugins marketplace
/plugin marketplace add shihwesley/shihwesley-plugins
/plugin install code-simplifier-tldr@shihwesley-plugins

# Or install directly from GitHub
/plugin install --source github shihwesley/code-simplifier-tldr
```

## Usage

```bash
# Simplify recently modified files
/simplify-tldr

# Simplify a specific file
/simplify-tldr src/api/auth.ts

# Simplify files matching a pattern
/simplify-tldr src/components/*.tsx
```

The agent can also be triggered automatically by Claude Code when code simplification tasks are detected.

## How it works

```
┌─────────────────────────────────────────────┐
│  1. Merkle check (if mercator-ai installed) │
│     docs/.mercator.json → what changed?     │
├─────────────────────────────────────────────┤
│  2. TLDR summaries for changed files        │
│     AST structure, ~200 tokens per file     │
├─────────────────────────────────────────────┤
│  3. Line-range reads for target sections    │
│     Only the functions you'll modify        │
├─────────────────────────────────────────────┤
│  4. Edit → Verify → Log                    │
│     Changes recorded in SIMPLIFICATION_LOG  │
└─────────────────────────────────────────────┘
```

**Token cost comparison (100-file codebase, 3 files changed):**

| Approach | Tokens |
|----------|--------|
| Read all files fully | ~250,000 |
| TLDR all files | ~20,000 |
| Merkle diff + TLDR changed | ~650 |

## What it does

- Reduces unnecessary complexity and nesting
- Eliminates redundant code and abstractions
- Improves naming and readability
- Follows project standards from CLAUDE.md
- Avoids nested ternaries — prefers explicit control flow
- Never changes behavior, only structure
- Logs every change to `SIMPLIFICATION_LOG.md`

## Components

| Type | File | Purpose |
|------|------|---------|
| Agent | `agents/code-simplifier.md` | Core simplifier with TLDR + merkle protocol |
| Command | `commands/simplify.md` | `/simplify` slash command entry point |

## Works with

- **mercator-ai** — Provides `docs/.mercator.json` merkle manifest for O(1) change detection. Optional but recommended.
- **TLDR read hook** — Intercepts file reads and returns AST summaries. The agent is built to consume these summaries natively.

## License

MIT
