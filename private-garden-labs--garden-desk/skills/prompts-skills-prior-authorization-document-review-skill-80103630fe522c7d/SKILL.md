---
name: prior-authorization-document-review
description: Prior-authorization packet completeness. Load after document-review. Use when this capability is needed.
metadata:
  author: Private-Garden-Labs
---

Without supplied payer requirements, list contents and ask for requirements. Never use remembered payer rules.

Map requirements to evidence. States: `documented`, `not documented`, `conflicting`, `not applicable`, `human review required`. Never use `met`, `failed`, `approve`, or `deny`. Missing evidence needs human review; it does not prove failure.

Record request/minimum patient identifiers, provider, payer, requested item as written, dates, and document types.

Table: requirement; state; source fact; location; missing/conflicting item; check. Make no medical-necessity, coverage, coding, or HIPAA-compliance claim.

---
> Source: [Private-Garden-Labs/garden-desk](https://github.com/Private-Garden-Labs/garden-desk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
