---
name: paper-refbib-stub
description: Convert normalized multi-search-engine results to minimal BibTeX, preserving real DOI, author, publication year, arXiv ID, source URL, and provenance metadata when available. Unknown years are omitted and duplicate DOI records collapse to one entry. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# paper-refbib-stub

Reads a `multi-search-engine` JSON document on stdin and emits a BibTeX file
of `@misc{}` entries keyed `ref1`, `ref2`, ... Caller wires the upstream
search output via `entrypoint.stdin`.

The converter consumes optional normalized `doi`, `authors`,
`corporate_authors`, and `year` fields, while retaining URL-based DOI/arXiv
detection for older producers. Corporate authors are protected with nested
BibTeX braces so institution names are not rearranged as personal names.
It never invents a publication year: missing or malformed years are omitted.
DOIs are normalized case-insensitively, and repeated DOI records emit only
the first entry so citation keys stay unique and deterministic.

All search-provided text fields are treated as untrusted plain text. Control
characters, backticks, embedded BibTeX entry fragments, backslashes, and
unbalanced braces are neutralized before field emission; structural URL
characters are percent-encoded without discarding Unicode locators. This keeps
truncated search snippets from corrupting the generated BibTeX database.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
