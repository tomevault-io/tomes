---
name: top-n-with-detail
description: > Use when this capability is needed.
metadata:
  author: dbt-labs
---

# Top-N with Detail

A bar chart ranking the top N categories by a metric, sitting beside a detail
table that exposes the same rows. One query powers both — add `ORDER BY metric
DESC LIMIT N` in the SQL so the data arrives pre-ranked.

## When to reach for this

- You have a "who/what is biggest?" question with a categorical dimension
- Row-level context matters (e.g., rank + order count + avg order value)
- The list is bounded and the user benefits from scanning the full ranked table

## When NOT to use this

- No natural ranking or comparison → plain `bar` chart
- Too many categories for a table (>50 rows) → add pagination or a filter
- Time-based ranking → pair with `time-series-trend` instead

## The pattern

```yaml
queries:
  top_products:
    sql: |
      SELECT product, SUM(revenue) AS revenue, COUNT(*) AS orders
      FROM orders
      GROUP BY product
      ORDER BY revenue DESC
      LIMIT 10

charts:
  ranking_bar:
    type: bar
    query: top_products
    x: product
    y: revenue
    title: Top Products by Revenue

  detail_table:
    type: table
    query: top_products
    title: Product Detail
    style:
      columns:
        product:
          label: Product
        revenue:
          label: Revenue
          format: "$,.0f"
        orders:
          label: Orders

rows:
  - cols: [ranking_bar, detail_table]
```

See `examples/top-n-with-detail.yml` for the inline-data worked example.

## Variations

| Variation | YAML knob | When |
|---|---|---|
| Color by category | `color: category_col` on the bar | Distinguish groups within the ranking |
| Horizontal bars | `type: bar` with long labels reads naturally as horizontal | Long category names |
| Click-through | add `link: "/detail?id={{ x }}"` to bar chart | Link to a per-item board |
| Tighter N | `LIMIT 5` | Space-constrained layouts |

## Common pitfalls

| Pitfall | Why it breaks | Fix |
|---|---|---|
| Forgetting `ORDER BY` | Arbitrary bar ordering | Always `ORDER BY metric DESC` |
| Two separate queries | Bar and table can diverge | Use one query for both |
| Too many bars (>15) | Bar chart unreadable | Set `LIMIT 10` or fewer |

## Worked example

See `examples/top-n-with-detail.yml` — top 5 products, bar + table, inline
data. No warehouse required.

## YAML Reference

For syntax and field details: {{ s_yaml_reference_footer }}

---
> Source: [dbt-labs/dbt-charts](https://github.com/dbt-labs/dbt-charts) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
