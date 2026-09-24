---
name: meta-pdf-reformat-pipeline
description: Modernize a legacy PDF: structural extraction → natural-language rewrite of problem pages → audit summary → re-merge into the final PDF. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# PDF Reformat Pipeline (Meta-Skill)

Historical-contract / scanned-manual / legal-document modernization in
4 steps: extract → rewrite → audit → re-merge. The `audit` step's output
gives a human reviewer a diff-summary before the merge is finalized.

## Fallback

Run pdf-toolkit extract → nano-pdf rewrite → summarize → pdf-toolkit merge
manually.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
