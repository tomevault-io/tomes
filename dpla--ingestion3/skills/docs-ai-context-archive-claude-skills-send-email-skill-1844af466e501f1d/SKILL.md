---
name: send-email
description: Send an ingest summary email to a hub's configured contacts from i3.conf using the most recent (or specified) mapping output. Use when user asks send/resend a hub ingest summary email. Use when this capability is needed.
metadata:
  author: dpla
---

# send-email
```bash
source .env && bash scripts/communication/send-ingest-email.sh $HUB
```

Pass `--yes` to skip the confirmation prompt. Pass a mapping dir path as a second argument to use a specific mapping output instead of the latest.

---
> Source: [dpla/ingestion3](https://github.com/dpla/ingestion3) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
