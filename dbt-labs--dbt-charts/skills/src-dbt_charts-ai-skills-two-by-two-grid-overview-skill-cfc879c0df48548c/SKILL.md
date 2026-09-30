---
name: two-by-two-grid-overview
description: > Use when this capability is needed.
metadata:
  author: dbt-labs
---

# Two-by-Two Grid Overview

Four charts arranged in a 2×2 grid, each with equal column width, giving users
a balanced multi-metric overview before diving into detail. Implemented as two
`rows:` of `cols:` with two items each — dbt charts splits the width evenly by
default.

## When to reach for this

- A board opens with a balanced overview ("revenue / cost / margin / users")
- All four charts have equal analytical importance
- Each chart answers a different question about the same domain

## When NOT to use this

- One chart is clearly the hero → enlarge it via `width:` or move it to its own row
- All four are KPI numbers → use `kpi-row` instead (it handles delta and format)
- More than 6 equally-weighted charts → split into tabs or multiple boards

## The pattern

```yaml
rows:
  - cols:
      - revenue_trend    # top-left
      - cost_trend       # top-right
  - cols:
      - by_region        # bottom-left
      - by_product       # bottom-right
```

No section title — the four labeled charts are self-explanatory, and a heading over them just repeats their titles.

Each chart is defined as usual in `charts:`. The 2×2 is purely a layout
decision — swap in any chart type per cell.

See `examples/two-by-two-grid-overview.yml` for the inline-data worked example.

## Variations

| Variation | YAML knob | When |
|---|---|---|
| 2×3 (six cells) | Add a third `cols:` row | Six equally-weighted metrics |
| Asymmetric | `width: "60%"` on one cell | Slightly more emphasis on one chart |
| Section title | `title:` on a `rows:` item | Rarely needed — only when a heading adds something the charts don't (a shared scope, a mode boundary). Default to omitting it |
| Grid layout | `grid: columns: 24` + `col_span: 12` | Finer column control |

## Common pitfalls

| Pitfall | Why it breaks | Fix |
|---|---|---|
| Charts with very different heights | Mismatched row heights look accidental | Use charts of the same type per row |
| All four showing the same metric | No additional insight | Ensure each cell answers a distinct question |
| Nesting cols in cols | Unexpected layout behavior | Use rows at the top level, cols inside rows |

## Worked example

See `examples/two-by-two-grid-overview.yml` — four charts (two line + two bar)
arranged 2×2 from two inline-data queries. No warehouse required.

## YAML Reference

For syntax and field details: {{ s_yaml_reference_footer }}

---
> Source: [dbt-labs/dbt-charts](https://github.com/dbt-labs/dbt-charts) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
