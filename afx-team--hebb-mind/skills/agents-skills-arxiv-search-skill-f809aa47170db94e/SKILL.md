---
name: arxiv-search
description: Use when working with the search topic or keywords
metadata:
  author: afx-team
---

# arxiv Paper Search

Search arxiv for academic papers related to the given query.

## Instructions

1. Use WebSearch to search for: `arxiv ${query}` and `arxiv ${query} 2024 2025 2026`
2. For each relevant paper found (up to 10), extract:
   - Title
   - Authors
   - Date
   - arxiv URL
   - Abstract summary (2-3 sentences)
   - Key contributions
3. Present results in a structured markdown table
4. Highlight papers most relevant to agent memory systems if applicable
5. Note any survey/review papers separately as they provide broader context

---
> Source: [afx-team/hebb-mind](https://github.com/afx-team/hebb-mind) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-14 -->
