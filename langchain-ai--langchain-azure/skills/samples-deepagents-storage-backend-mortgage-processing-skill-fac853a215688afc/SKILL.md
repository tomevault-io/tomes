---
name: packet-intake
description: Check a mortgage packet manifest and write /output/01-packet-index.json. Use when this capability is needed.
metadata:
  author: langchain-ai
---

# Packet Intake

Read `/source/packet-manifest.json` and compare the available documents with its expected
document list.

This skill produces exactly one artifact: `/output/01-packet-index.json`. Use that exact
path; do not rename it or create a subdirectory.

The artifact contains:

- `packet_id`
- `documents`, with one entry per available document containing its file name and page range
- `missing_documents`

Use only facts present in the manifest. Keep the output concise and valid JSON.

---
> Source: [langchain-ai/langchain-azure](https://github.com/langchain-ai/langchain-azure) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
