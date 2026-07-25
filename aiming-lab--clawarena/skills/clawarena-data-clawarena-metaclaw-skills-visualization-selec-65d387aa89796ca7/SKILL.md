---
name: visualization-selection
description: Use this skill when creating charts, plots, or dashboards. Choose the visualization type that best communicates the data relationship before writing any plotting code.
metadata:
  author: aiming-lab
---

# Visualization Selection Guide

| Goal | Chart Type |
|------|------------|
| Compare categories | Bar chart (horizontal if many labels) |
| Show distribution | Histogram, box plot, violin plot |
| Show trend over time | Line chart |
| Show correlation | Scatter plot, heatmap |
| Show part-to-whole | Pie (<=5 slices), stacked bar |

**Principles:**
- Label axes and include units.
- Use color purposefully — not just for decoration.
- Avoid 3D charts; they distort perception.
- Start y-axis at 0 for bar charts (truncated bars mislead).
- Use a colorblind-safe palette (e.g., `viridis`, `colorbrewer`).

---
> Source: [aiming-lab/ClawArena](https://github.com/aiming-lab/ClawArena) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
