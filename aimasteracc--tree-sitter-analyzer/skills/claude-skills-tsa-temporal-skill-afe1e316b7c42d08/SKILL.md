---
name: tsa-temporal
description: | Use when this capability is needed.
metadata:
  author: aimasteracc
---

# tsa-temporal — Hot zones via git history

> Per-symbol modification frequency persisted in `ast_symbol_activation`.
> Computed from `git log --follow -p -U0` hunk attribution at index time.
> Symbols with `mod_count_30d >= 5` auto-trigger CAUTION in `edit action=impact`.

## When to use

| Goal                                  | How                                                         |
|---------------------------------------|-------------------------------------------------------------|
| Hot-zone caller fanout                | `nav action=callers function_name="X" include_activation=true` |
| Hot-zone callee fanout                | `nav action=callees function_name="X" include_activation=true` |
| "Is this commit touching hot zones?"  | `edit action=impact` — read `risk_factors`                  |
| Single-file recent churn              | `health action=file` — read `git_hotspot` dim               |

**Don't use** when:
- The question is static (e.g. "who calls X") — use `tsa-graph` skill
- File is brand new (no git history) — temporal data will be all-zero

## Procedure

### Pre-refactor hot-zone scan

For each symbol you're about to refactor:

```
nav action=callers function_name="X" include_activation=true limit=50
```

Returns enriched entries:
```yaml
callers: [
  {
    name: ...,
    file: ...,
    line: ...,
    callee_resolution: ...,
    activation: {
      mod_count_30d: <int>,
      last_modified_at: <unix ts>
    }
  }, ...
]
```

Filter `mod_count_30d >= 5` to find the callers that have been modified
recently — those are the high-risk integration points for your refactor.

### Change-impact gate (catches hot zones automatically)

`edit action=impact` already includes hot-zone detection. Look for this
in the risk_factors:

```yaml
risk_factors: [
  {
    factor: hot_zone | activation,
    reason: "hot zone: file_path:symbol modified 12× in 30d, request extra review",
    severity: caution
  }
]
```

The verdict bumps to CAUTION when ≥1 changed-file symbol has
`mod_count_30d >= 5`.

### Long-tail vs hot-zone heuristic

| 30d count | Meaning                                |
|-----------|----------------------------------------|
| 0         | Cold — stable code, low refactor risk  |
| 1-4       | Normal activity                        |
| 5-10      | Hot zone — extra review attention      |
| 10-20     | Refactor pressure — may need redesign  |
| 20+       | Churn signal — possibly architectural problem |

## Index-time controls

- Default: temporal activation auto-computed on every `index_file`
- Opt-out: `TSA_INDEX_ACTIVATION=0 uv run tree-sitter-analyzer ...`
- Workers don't run git (writer-thread only) — safe under parallel index

## Storage

Table `ast_symbol_activation` (one row per symbol_id):
```
symbol_id, file_path, last_modified_commit, last_modified_at,
mod_count_30d, mod_count_90d, mod_count_all, computed_at, git_state
```

`git_state` ∈ `{tracked, untracked, shallow, no_repo}` — degrades gracefully
on shallow clones (CI), untracked files, or non-repo paths.

## Reading `git_state`

- `tracked` → counts accurate
- `shallow` → counts may be undercounts (shallow clone)
- `untracked` / `no_repo` → all counts 0; symbol exists but has no history

## CLI access (today, indirect)

There is no dedicated `--temporal` CLI flag yet. Access via:
```bash
uv run tree-sitter-analyzer --callees <FUNC> --output-format json | jq '.callees[] | select(.activation.mod_count_30d >= 5)'
```

Or query the SQLite DB directly for batch reports:
```bash
# Portable: stdlib sqlite3 via `uv run python` (the `sqlite3` CLI is
# frequently absent from PATH on Windows).
uv run python -c "
import sqlite3
sql = '''
SELECT s.name, s.file_path, a.mod_count_30d
FROM ast_symbol_activation a
JOIN ast_symbol_rows s ON s.id = a.symbol_id
WHERE a.mod_count_30d >= 5
ORDER BY a.mod_count_30d DESC LIMIT 20'''
for r in sqlite3.connect('.ast-cache/index.db').execute(sql):
    print(*r, sep='\t')
"
```

## Anti-patterns

- Don't compare `mod_count_all` across symbols added at different times — older
  symbols win mechanically. Use `mod_count_30d` for fair churn comparison.
- Don't refactor a low-30d, high-all symbol — that's stable code; touching
  it has high blast radius for low benefit.
- Don't ignore `git_state=shallow` — in CI you'll see misleading low counts.

## Decision surface

```yaml
include_activation=true response addition (per callee/caller entry):
  activation:
    mod_count_30d: <int>
    last_modified_at: <unix ts | null>

edit action=impact addition:
  risk_factors: [{factor: "hot_zone", reason: "...mod_count_30d=N...", severity: "caution"}]
  verdict: CAUTION   # bumped from SAFE/REVIEW when hot zone touched
```

---
> Source: [aimasteracc/tree-sitter-analyzer](https://github.com/aimasteracc/tree-sitter-analyzer) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
