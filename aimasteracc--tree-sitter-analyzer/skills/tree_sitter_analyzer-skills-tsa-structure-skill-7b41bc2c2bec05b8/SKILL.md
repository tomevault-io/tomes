---
name: tsa-structure
description: | Use when this capability is needed.
metadata:
  author: aimasteracc
---

# tsa-structure — File shape without the file body

## Tool routing

| Question                                        | Tool                         |
|-------------------------------------------------|------------------------------|
| Outline / table of classes + methods            | `structure action=analyze`   |
| Run a tree-sitter query (e.g., all `def` nodes) | `search action=query`        |
| Detect design patterns (singleton, factory, …)  | `health action=patterns`     |
| Classify a diff (refactor vs feature vs fix)    | `edit action=classify`       |

## Procedure

### File outline (most common)

```yaml
structure action=analyze file_path="tree_sitter_analyzer/health_scorer.py"
# returns: {classes: [...], functions: [...], imports: [...]}
```

For a markdown-formatted table:

```bash
uv run tree-sitter-analyzer <file> --table full
```

### Custom tree-sitter query

When you need something the built-in tools don't surface:

```yaml
search action=query file_path="..." query_key="class"
# OR
search action=query file_path="..." query_string="(decorated_definition) @decorated"
```

`--list-queries` (CLI) shows all built-in queries available per language.

### Diff classification

```yaml
edit action=classify file_path="..." before_hash="abc" after_hash="def"
# returns: {classification: "refactor|feature|bugfix|test|docs|chore", confidence: 0.92}
```

Useful for PR descriptions and CHANGELOG categorization.

### Pattern detection

```yaml
health action=patterns file_path="..." patterns=["singleton", "factory", "observer"]
```

## CLI equivalents

```bash
uv run tree-sitter-analyzer <file> --table full           # outline
uv run tree-sitter-analyzer <file> --query-key class      # built-in query
uv run tree-sitter-analyzer <file> --query-string "(...)" # custom query
uv run tree-sitter-analyzer <file> --code-patterns
uv run tree-sitter-analyzer --semantic-classify           # edit action=classify
```

## Anti-patterns

- DON'T read the whole file just to find "what classes are in it" — use the structure tool
- DON'T write a custom tree-sitter query when `structure action=analyze` covers it
- DON'T use `edit action=classify` on huge multi-purpose commits — split them first

---
> Source: [aimasteracc/tree-sitter-analyzer](https://github.com/aimasteracc/tree-sitter-analyzer) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
