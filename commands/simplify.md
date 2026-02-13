---
description: "TLDR-aware code simplifier — uses AST summaries for context, saves 80%+ tokens"
argument-hint: "[file or pattern]"
allowed-tools: ["Read", "Write", "Edit", "Glob", "Grep", "Bash", "Task"]
---

# TLDR-Aware Code Simplifier

Launch the TLDR-optimized code simplifier agent to refine recently modified code.

## How It Works

This simplifier is **TLDR-aware**:
1. Uses AST summaries to survey the codebase (saves ~95% tokens)
2. Requests specific line ranges only for code it will modify
3. Preserves full context while minimizing token consumption
4. **Auto-logs** all changes to `SIMPLIFICATION_LOG.md` in project root

When the mercator-ai plugin is installed, it also uses the merkle manifest for O(1) change detection — skipping files that haven't changed since the last mapping.

## Usage

```bash
# Simplify recently modified files
/simplify

# Simplify specific file
/simplify src/api/auth.ts

# Simplify pattern
/simplify src/components/*.tsx
```

## Agent Instructions

You are now operating as the **TLDR-aware code simplifier**. Follow the protocol defined in the code-simplifier-tldr agent:

1. **Context**: Check for `docs/CODEBASE_MAP.md` and `docs/.mercator.json`
2. **Discovery**: Use TLDR summaries to understand file structures
3. **Target**: Request line ranges for sections you'll modify
4. **Simplify**: Apply project standards and clarity improvements
5. **Verify**: Confirm changes with targeted reads
6. **Log**: Write/append session summary to `SIMPLIFICATION_LOG.md`

$ARGUMENTS

Begin by checking what files were recently modified with `git diff --name-only HEAD~3`, then survey them using TLDR summaries before diving into specific sections.
