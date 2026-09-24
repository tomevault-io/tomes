---
name: paper-delivery-summary
description: Deterministic final delivery summary for meta-paper-write. Reports only verified PDF compilation fields and the exact citation-map SUMMARY statistics. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# Paper delivery summary

Internal deterministic delivery formatter for `meta-paper-write`. It accepts
the paper contract, the runtime language instruction, `compile_pdf` output,
and `citation_map` output as JSON. It fails closed unless the PDF markers and
the complete, internally consistent citation `SUMMARY` are machine-readable.

The formatter never calls an LLM and never infers page or citation counts from
prose. Chinese and English delivery text is selected from the confirmed paper
language contract, cross-checked against the runtime language instruction.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
