# code-simplifier-tldr

Claude Code plugin that simplifies code using TLDR-aware AST summaries. Reads structure first via lightweight summaries, then targets only the files that need changes. Saves 80%+ tokens compared to reading every file fully.

## Install

```bash
/plugin marketplace add shihwesley/shihwesley-plugins
/plugin install code-simplifier-tldr@shihwesley-plugins
```

Or install directly:

```bash
/plugin install --source github shihwesley/code-simplifier-tldr
```

## How it works

The plugin provides a `code-simplifier-tldr` agent that:

1. Reads files through TLDR, getting AST summaries (~150 tokens vs ~2500 for a 500-line file)
2. Identifies which sections need simplification from the summary
3. Requests only those line ranges for full content
4. Applies refinements with minimal token spend

## What it does

- Reduces unnecessary complexity and nesting
- Eliminates redundant code and abstractions
- Improves naming and readability
- Follows project standards from CLAUDE.md
- Never changes behavior, only structure

## License

MIT
