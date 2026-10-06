---
name: medical-record-timeline
description: Administrative medical timeline. Load after document-review. Use when this capability is needed.
metadata:
  author: Private-Garden-Labs
---

Use minimum patient identifiers. Extract event dates/times, types, providers/facilities, recorded actions, and locations. Distinguish authored, signed, ordered, collected, resulted, service, admission, discharge, and received dates.

Sort by supported dates; separate undated records. Label inferred order `sequence inferred from supplied records` and explain its basis. Do not infer clinical meaning, causation, urgency, or missing events.

Table: date/range; recorded event; provider/facility; source fact; location; status/conflict. Do not interpret diagnoses, tests, treatments, or medications, or claim HIPAA compliance.

---
> Source: [Private-Garden-Labs/garden-desk](https://github.com/Private-Garden-Labs/garden-desk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
