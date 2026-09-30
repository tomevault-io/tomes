---
name: before-after-comparison
description: > Use when this capability is needed.
metadata:
  author: dbt-labs
---

# Before-After Comparison

Two series rendered on the same bar or line chart, sharing the x-axis, so the
viewer can compare baseline vs current or plan vs actual across categories or
time periods. Use `y: [series_a, series_b]` for layered bars, or `color:` for
grouped multi-series.

## When to reach for this

- "How does Q4 compare to Q3 for each region?"
- "Are we above or below plan by category?"
- The comparison dimension is the same set of x values for both series

## When NOT to use this

- Trend over time on a single metric → `time-series-trend`
- More than 3 series → too cluttered; split into separate charts
- Composition (parts of a whole) → stacked area in `faceted-small-multiples`

## The pattern

```yaml
queries:
  plan_vs_actual:
    sql: |
      SELECT category,
             SUM(actual_revenue)  AS actual,
             SUM(planned_revenue) AS plan
      FROM budget
      GROUP BY category
      ORDER BY actual DESC

charts:
  comparison:
    type: bar
    query: plan_vs_actual
    x: category
    y: [actual, plan]        # two series, same x
    title: Actual vs Plan by Category
```

For time-based comparisons, use two separate columns in one query and map with
`color:` instead:

```yaml
queries:
  by_month:
    columns: [month, current, prior]
    values: ...

charts:
  trend_compare:
    type: line
    query: by_month
    x: month
    y: [current, prior]
    title: Current vs Prior Period
```

See `examples/before-after-comparison.yml` for the inline-data worked example.

## Variations

| Variation | YAML knob | When |
|---|---|---|
| Layered bars | `y: [a, b]` | Side-by-side bars per category |
| Two line series | `y: [a, b]` on `type: line` | Time-based trend comparison |
| Multiple categories | keep `x:` categorical | Natural for department/region comparisons |
| Delta column | add a computed delta in SQL | Explicitly show the gap |

## Common pitfalls

| Pitfall | Why it breaks | Fix |
|---|---|---|
| Series on different scales | Misleading visual; one series dwarfs the other | Use matching units or a secondary axis |
| Too many series (`y: [a, b, c, d]`) | Legend and bars both unreadable | Cap at 2–3 series; combine the rest |
| Different x-values per series | Chart gaps or misaligned bars | Ensure both series have a value for every x |
| Swapped series order | Baseline visually dominates current | Put the primary/current series first in `y:` |

## Worked example

See `examples/before-after-comparison.yml` — four departments comparing
current vs baseline spend. Inline data, no warehouse needed.

## YAML Reference

For syntax and field details: {{ s_yaml_reference_footer }}

---
> Source: [dbt-labs/dbt-charts](https://github.com/dbt-labs/dbt-charts) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
