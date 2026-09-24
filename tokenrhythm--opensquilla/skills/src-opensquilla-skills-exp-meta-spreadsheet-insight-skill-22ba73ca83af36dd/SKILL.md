---
name: meta-spreadsheet-insight
description: Turn an Excel workbook into business insight: structured read → trend/anomaly summary → write back to a new 'Insights' sheet → persist KPIs to memory. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# Spreadsheet Insight (Meta-Skill)

Reads a workbook, computes a structured trend / anomaly analysis, writes
the result back as a new sheet, and persists key KPIs to long-term memory.

## Fallback

LLM should call xlsx read, summarize, xlsx append, then `memory_save`.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
