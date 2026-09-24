---
name: paper-citation-integrity-gate
description: Deterministic citation-count and provenance gate for meta-paper-write. Checks the citation_map summary against the numeric paper citation target without trusting an LLM verdict. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# Paper citation integrity gate

Internal deterministic gate used after `citation_map`. It parses the requested
integer citation target and the map's machine-readable `SUMMARY`, then blocks
when distinct cited keys are below target or any cited entry is invalid or
weak. Unused bibliography entries are reported as a warning, not a blocker.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
