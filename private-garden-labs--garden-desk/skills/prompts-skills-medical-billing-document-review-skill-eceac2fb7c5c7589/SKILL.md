---
name: medical-billing-document-review
description: Administrative comparison of medical bills and claims. Load after document-review. Use when this capability is needed.
metadata:
  author: Private-Garden-Labs
---

Extract minimum patient identifiers, claim/bill identifiers, provider, payer, service date/place/description, code, units, charge, allowed amount, payment, adjustment, denial text, and order reference.

Recalculate amounts. Report missing support, patient/provider/date conflicts, code/unit/amount differences, and unmatched records. `not documented` is not a conflict. Do not assume current codes, rates, edits, or payer/coverage rules.

Table: category; record identifier; sources/values; difference; check. Do not validate codes, decide coverage/payment, or claim HIPAA compliance.

---
> Source: [Private-Garden-Labs/garden-desk](https://github.com/Private-Garden-Labs/garden-desk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
