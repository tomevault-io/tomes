---
name: pdf-reader
description: Extract text from PDF files. Use when reading, parsing, or analyzing PDFs. Use when this capability is needed.
metadata:
  author: alibaba
---

# PDF Reader

Run `scripts/read_pdf.py` relative to this skill's directory.

```bash
python3 SKILL_DIR/scripts/read_pdf.py -f <pdf_path> [options]
```

Options: `-p "1-5,7"` page range, `--format json` structured output, `--metadata` include doc info, `-m 8000` max chars.

Setup: `pip install PyMuPDF`

---
> Source: [alibaba/anolisa](https://github.com/alibaba/anolisa) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-12 -->
