---
name: paper-latex-sanitizer
description: Deterministically normalize safe LaTeX punctuation and replace unsupported forecast magnitudes with explicit placeholders before meta-paper-write publication gates run. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# Paper LaTeX sanitizer

Internal deterministic pre-publication sanitizer for `meta-paper-write`.
It runs before the length, citation, and publication-quality gates.

The sanitizer performs only two bounded repairs:

- normalize U+2011, U+2013, and isolated U+2014 punctuation to LaTeX-safe
  ASCII equivalents while preserving paired Chinese em dashes (`——`);
- when `EVIDENCE_STATUS: not_supplied`, replace concrete forecast magnitudes
  in results-facing sections with `TBD` / `待实验确定`. Planned setup values
  remain intact. A declared result threshold remains intact only when the same
  magnitude is present in the authoritative user request/paper contract;
  labeling an invented number as a target or hypothesis does not preserve it;
- remove only the known generated `figure_placeholder_template` or
  `table_placeholder_template` input line when the same manuscript already
  contains the corresponding inlined figure/table environment. Arbitrary user
  `\input{...}` commands and non-redundant template inputs remain untouched.

For an artifact-backed package, the referenced `MANUSCRIPT_PATH` is replaced
atomically and the compact manifest is returned. Inline manuscript packages
are normalized in the returned package. This step is not a quality gate: the
independent `paper-quality-gate` must still run afterwards and block any
unsupported semantic claims that remain.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
