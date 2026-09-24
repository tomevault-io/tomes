---
name: meta-pdf-intelligence
description: Use this meta-skill instead of answering directly when the user needs PDF analysis, pasted PDF excerpt analysis, digesting, comparison, or question answering that benefits from multi-skill orchestration across PDF extraction, summarization, cross-document synthesis, traceable evidence indexing, and memory capture.
metadata:
  author: TokenRhythm
---

# PDF Intelligence (Meta-Skill)

Process one or more PDFs into a traceable analysis entry. The workflow first
classifies the request, preserves file/page evidence, synthesizes across
documents when needed, and stores a structured memory index.

## Fallback

LLM should manually run `pdf-toolkit` scripts then summarize and
`memory_save`.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
