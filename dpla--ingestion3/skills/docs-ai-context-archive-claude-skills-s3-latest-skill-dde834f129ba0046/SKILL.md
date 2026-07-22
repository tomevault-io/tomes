---
name: s3-latest
description: Find the latest harvest/mapping/jsonl exports in S3 for a given hub (under s3://dpla-master-dataset/<hub>/...). Use when user asks latest S3 data for a hub, when a hub was last ingested, check whether mapping/jsonl/harvest exists in S3, or latest jsonl/mapping/harvest for a hub. Use when this capability is needed.
metadata:
  author: dpla
---

# s3-latest
```bash
source .env && bash scripts/status/s3-latest.sh $HUB
```

---
> Source: [dpla/ingestion3](https://github.com/dpla/ingestion3) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
