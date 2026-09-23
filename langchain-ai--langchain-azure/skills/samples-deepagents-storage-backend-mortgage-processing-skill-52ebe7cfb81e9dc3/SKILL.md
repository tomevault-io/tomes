---
name: mortgage-underwriting
description: Apply mortgage policy and write /output/04-underwriting-decision.md. Use when this capability is needed.
metadata:
  author: langchain-ai
---

# Mortgage Underwriting

Read these files, preferably in parallel:

- `/output/03-extracted-facts.json`
- `/output/01-packet-index.json`
- `/source/underwriting-policy.md`

Calculate loan-to-value using the lower of purchase price or appraised value. Calculate
debt-to-income using verified monthly income. Verify assets and identify missing documents.

This skill produces exactly one artifact: `/output/04-underwriting-decision.md`. Use that
exact path; do not rename it or create a subdirectory.

The artifact has concise sections named:

- Decision
- Calculations
- Conditions
- Evidence

Cite `/source/` paths for factual evidence. Apply policy from the packet rather than
embedding policy assumptions in the decision.

---
> Source: [langchain-ai/langchain-azure](https://github.com/langchain-ai/langchain-azure) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
