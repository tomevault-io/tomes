---
name: send-email
description: Send an email. Use when this capability is needed.
metadata:
  author: DenisovAV
---

# Send email

## Instructions

Call the `run_intent` tool with the following exact parameters:

- intent: send_email
- parameters: A JSON string with the following fields:
  - extra_email: the email address to send the email to. String.
  - extra_subject: the subject of the email. String.
  - extra_text: the body of the email. String.

---
> Source: [DenisovAV/flutter_edge_ai](https://github.com/DenisovAV/flutter_edge_ai) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
