---
name: report
description: Generate evolution report Use when this capability is needed.
metadata:
  author: DataLab-atom
---

# /report — Evolution Report

1. Call `evo_get_status` for current state
2. For each target, call `evo_get_lineage` on its best branch
3. Read `memory/global/long_term.md` for accumulated insights
4. Read `memory/synergy/records.md` for cross-function results
5. `exec git -C <repo> log --graph --oneline --all` for visual lineage

Generate a Markdown report:

```markdown
## Evolution Summary
- Generations: {N}
- Total evaluations: {total_evals}
- Seed baseline: {seed_obj}
- Best overall: {best_obj_overall} ({improvement})

## Per-Target Results
| Target | Seed | Best | Improvement | Key Generation |
|--------|------|------|-------------|----------------|
| ...    | ...  | ...  | ...         | ...            |

## Key Breakthroughs
- Gen {N}: {target} — {what changed} ({delta})

## Synergy Results
- {targetA} × {targetB}: {result}

## Lessons Learned
{from long_term memory}

## Failed Approaches
{from failures.md}

## Evolution Tree
{git log graph}
```

---
> Source: [DataLab-atom/EvoAny](https://github.com/DataLab-atom/EvoAny) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
