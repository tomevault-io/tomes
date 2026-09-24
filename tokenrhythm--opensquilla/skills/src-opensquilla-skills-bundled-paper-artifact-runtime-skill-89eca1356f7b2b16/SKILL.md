---
name: paper-artifact-runtime
description: Internal cross-platform artifact persistence, assembly, citation-audit, and PDF compilation runtime for meta-paper-write. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# Paper artifact runtime

Internal deterministic runtime for `meta-paper-write`. It accepts one JSON
object on standard input with an `operation` field and performs exactly one of
these operations inside the orchestrator-owned workspace:

- `persist_sections`
- `assemble_manuscript_tex`
- `materialize_manuscript`
- `apply_length_expansion`
- `citation_map`
- `compile_pdf`

The runtime validates the runtime-owned MetaSkill run identifier, rejects
symlinked artifact roots and files, and keeps every artifact under
`paper/<meta_run_id>/`. PDF compilation invokes the managed `xelatex` and
`bibtex` executables with a platform-neutral argument vector, disables TeX
shell escape, applies paranoid Kpathsea file access, and verifies the real PDF
page count and final LaTeX quality log before returning success markers. Length
repair accepts at most one bounded body-only fragment per stable repair id,
rejects commands that could alter document boundaries, citations, or external
inputs, and applies it idempotently inside the run-owned manuscript.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
