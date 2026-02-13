# Changelog

## 2.0.0 — 2026-02-13

### Added
- Merkle manifest integration for O(1) change detection (reads `docs/.mercator.json`)
- Pre-simplification context check (codebase map, docs folder scan)
- `/simplify` slash command with file/pattern arguments
- L1-L3 TLDR summary support (type annotations, docstrings, constants)
- Session logging to `SIMPLIFICATION_LOG.md`
- Token budget comparison tables (merkle vs non-merkle workflows)

### Changed
- Agent upgraded from basic TLDR to merkle-enhanced TLDR protocol
- Plugin manifest now includes full metadata (homepage, keywords, author URL)

## 1.0.0 — 2025-01-10

### Added
- Initial release with TLDR-aware code simplifier agent
- AST summary-based file discovery
- Line-range targeting for modifications
- Core simplification principles (preserve behavior, enhance clarity, maintain balance)
