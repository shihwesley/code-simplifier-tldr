# CLAUDE.md

## Codebase Overview

Claude Code plugin that simplifies code through a three-tier token-optimization strategy: merkle diff (O(1) change detection), TLDR AST summaries (95% savings), and line-range targeting. Ships as an agent + slash command pair.

**Stack**: Markdown-based Claude Code plugin (agent definition + command entry point)
**Structure**: `agents/` (core protocol), `commands/` (CLI entry), `.claude-plugin/` (manifest)

For detailed architecture, see [docs/CODEBASE_MAP.md](docs/CODEBASE_MAP.md).
