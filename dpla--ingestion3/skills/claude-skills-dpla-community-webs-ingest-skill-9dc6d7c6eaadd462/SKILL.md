---
name: dpla-community-webs-ingest
description: Run Community Webs ingest. Use when the user says harvest community-webs, run community-webs ingest, export community webs, or process community webs DB. Use when this capability is needed.
metadata:
  author: dpla
---

# DPLA Community Webs Ingest

Community Webs ingest is handled by the **`dpla-hub-ingest`** skill with `community-webs` as the hub name.

The pre-processing step (SQLite DB → JSONL → ZIP → i3.conf update) runs entirely on EC2 via SSM — no local steps needed. See the **Community Webs Pre-processing** section in the `dpla-hub-ingest` skill for the full procedure.

**Trigger phrase to use:** "ingest community-webs" or "harvest community-webs"

---
> Source: [dpla/ingestion3](https://github.com/dpla/ingestion3) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
