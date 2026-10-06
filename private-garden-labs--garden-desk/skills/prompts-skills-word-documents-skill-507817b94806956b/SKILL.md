---
name: word-documents
description: Create or edit DOCX. Use read for DOC/DOCX text. Use when this capability is needed.
metadata:
  author: Private-Garden-Labs
---

Use `python-docx`; output DOCX, never DOC.

```python
from docx import Document

doc = Document()  # Document(path) to edit
doc.add_heading("Title", 0)
doc.add_paragraph("Body text.")
path = "/workspace/result.docx"
doc.save(path)
```

Reopen with `Document(path)`; compare content with the request. Check tables in `doc.tables` separately from `doc.paragraphs`. Return after a successful check.

---
> Source: [Private-Garden-Labs/garden-desk](https://github.com/Private-Garden-Labs/garden-desk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
