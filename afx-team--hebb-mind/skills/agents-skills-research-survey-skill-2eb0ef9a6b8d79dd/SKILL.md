---
name: research-survey
description: Output file path for the survey report (default writes to repo_pages/surveys/) Use when this capability is needed.
metadata:
  author: afx-team
---

# Research Survey

Conduct a comprehensive research survey combining academic and open-source sources.

## Instructions

1. **Academic Search**: Use WebSearch to find 5-10 recent papers on `${topic}` from arxiv, ACL, NeurIPS, ICML, etc.
2. **Open Source Search**: Use WebSearch to find top GitHub repos related to `${topic}` (sort by stars, recency)
3. **Industry Search**: Look for blog posts, technical reports from major AI labs (OpenAI, Anthropic, Google, Meta)
4. **Synthesize** findings into a structured report:
   - Executive Summary
   - Academic Landscape (key papers, trends)
   - Open Source Landscape (key projects, comparisons)
   - Industry Trends
   - Gap Analysis
   - Recommendations
5. Write the report to `${output}` or `repo_pages/surveys/${topic}-survey.md` if no output specified
6. Use markdown tables for comparisons, include all source links

---
> Source: [afx-team/hebb-mind](https://github.com/afx-team/hebb-mind) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-14 -->
