---
name: meta-multi-format-export-pack
description: From one piece of source content, render four deliverables: .docx report, .pptx slides, .xlsx data, and an HTML/PDF public version. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# Multi-Format Export Pack (Meta-Skill)

Renders one source content into four deliverables for different audiences:
- `.docx` — detailed report
- `.pptx` — slide deck
- `.xlsx` — data breakdown
- `.pdf` — public-facing print version

MVP runs the four renders **sequentially** (after the shared `model` step);
true parallel fan-out is future work (M7 in the proposal).

## Fallback

LLM should manually summarize first, then call docx / pptx / xlsx /
html-to-pdf in order.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
