---
name: pdf-reader
description: Extract text from PDF files. Use when reading, parsing, or analyzing PDFs. Use when this capability is needed.
metadata:
  author: agentic-os-org
---

# PDF Reader

Run `scripts/read_pdf.py` relative to this skill's directory.

```bash
python3 SKILL_DIR/scripts/read_pdf.py -f <pdf_path> [options]
```

Options: `-p "1-5,7"` page range, `--format json` structured output, `--metadata` include doc info, `-m 8000` max chars.

Setup: `pip install PyMuPDF`

---
> Source: [agentic-os-org/ANOLISA](https://github.com/agentic-os-org/ANOLISA) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-18 -->
