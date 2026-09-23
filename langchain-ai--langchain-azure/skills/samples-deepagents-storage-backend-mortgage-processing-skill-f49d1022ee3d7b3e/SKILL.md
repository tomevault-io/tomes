---
name: document-classification
description: Classify mortgage documents and write /output/02-classification.json. Use when this capability is needed.
metadata:
  author: langchain-ai
---

# Document Classification

Read `/source/packet-manifest.json` and classify every listed source file.

This skill produces exactly one artifact: `/output/02-classification.json`. Use that exact
path; do not rename it or create a subdirectory.

The artifact contains:

- `packet_id`
- `documents`, with one entry per source file containing `file`, `document_type`, and
  `confidence`

Use the manifest and file names as evidence. Keep the output concise and valid JSON.

---
> Source: [langchain-ai/langchain-azure](https://github.com/langchain-ai/langchain-azure) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
