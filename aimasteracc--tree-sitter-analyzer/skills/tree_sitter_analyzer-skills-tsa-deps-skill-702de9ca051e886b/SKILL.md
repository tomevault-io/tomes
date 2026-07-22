---
name: tsa-deps
description: | Use when this capability is needed.
metadata:
  author: aimasteracc
---

# tsa-deps — Imports & module topology

## Tool routing

| Question                                | Tool                              |
|-----------------------------------------|-----------------------------------|
| One file's direct deps                  | `health action=deps`              |
| Project-wide import graph (who imports whom) | `health action=imports`      |
| Project topology (entry points, hubs)   | `structure action=sitemap`        |

## Procedure

### File-level deps

```yaml
health action=deps file_path="tree_sitter_analyzer/ast_cache.py" mode="file_deps"
# returns: {imports: [...], imported_by: [...], depth: 2}
```

`mode` options:
- `summary` — project-wide dependency summary (alias: `full`)
- `file_deps` — one file's graph (requires `file_path`)
- `blast_radius` — impact set for a file (alias: `blast`; requires `file_path`)
- `cycles` — circular dependencies

### Import graph (project-level)

```yaml
health action=imports language="python" limit=50
# returns: ranked list of import hubs + leaves
```

Use to find:
- **Hubs** (many things import this) — high blast radius if changed
- **Leaves** (no one imports this) — possibly dead, or a CLI entry point
- **Cycles** — circular imports needing breaking

### Sitemap

```yaml
structure action=sitemap
# returns: {entry_points: [...], hub_modules: [...], leaf_modules: [...]}
```

Useful as a "first look" right after `tsa-landing`.

## CLI equivalents

```bash
uv run tree-sitter-analyzer <file> --dependencies file_deps
uv run tree-sitter-analyzer --dependencies summary
uv run tree-sitter-analyzer --import-graph --import-graph-mode summary
uv run tree-sitter-analyzer --codegraph-sitemap
```

## Anti-patterns

- DON'T grep for `^import` / `^from` to build a graph — incomplete (misses
  conditional / lazy imports captured by the AST)
- DON'T worry about leaves at the start — they're often legitimate (CLI mains,
  examples). Focus on hubs.
- DON'T extract a hub module without first checking its `imported_by` list
  — you'll break dozens of callers.

---
> Source: [aimasteracc/tree-sitter-analyzer](https://github.com/aimasteracc/tree-sitter-analyzer) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
