---
name: data-report
description: Use this skill when the task involves analyzing data to compute statistics, aggregations, or summaries, and presenting the results as a report. Suitable for tasks like "summarize this dataset", "calculate averages and totals", "generate a weekly sales report", or "show me trends in this data". Do NOT use for simple format conversion between file types.
metadata:
  author: agentscope-ai-java
---
# Data Report Skill

Analyzes structured data and generates statistical summary reports.

## Available Scripts

- `scripts/summarize.py` — Compute descriptive statistics (count, mean, min, max, stddev) for numeric columns and output a Markdown report

## Usage

```
python3 scripts/summarize.py --input data.csv --output report.md
```

---
> Source: [agentscope-ai-java/agentscope-java](https://github.com/agentscope-ai-java/agentscope-java) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
