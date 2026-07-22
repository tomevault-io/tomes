---
name: pdf
description: Process and extract content from PDF files Use when this capability is needed.
metadata:
  author: lwmxiaobei
---

# PDF Processing

To work with PDF files:

1. Use `bash` to check if `pdftotext` is available: `which pdftotext`
2. If not installed, suggest: `brew install poppler` (macOS) or `apt install poppler-utils` (Linux)
3. Extract text: `pdftotext input.pdf -` (outputs to stdout)
4. For structured extraction: `pdftotext -layout input.pdf -`
5. For page-specific extraction: `pdftotext -f 1 -l 5 input.pdf -` (pages 1-5)

For PDF metadata: `pdfinfo input.pdf`
For PDF to images: `pdftoppm -png input.pdf output_prefix`

---
> Source: [lwmxiaobei/xbcode](https://github.com/lwmxiaobei/xbcode) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
