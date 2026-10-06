---
name: dns-command-and-control-investigation
description: Analyze suspicious DNS behavior such as high entropy, beaconing, rare domains, unusual record types, and query volume. Distinguish indicators from confirmed C2 and recommend safe validation. Use when this capability is needed.
metadata:
  author: Sec-Link
---
# DNS command and control investigation

Analyze suspicious DNS behavior such as high entropy, beaconing, rare domains, unusual record types, and query volume. Distinguish indicators from confirmed C2 and recommend safe validation.

Output requirements:
- Cite observed evidence from the ticket.
- Mark unknown values as unavailable.
- Return structured JSON fields when requested.
- Do not change ticket status or execute commands.

---
> Source: [Sec-Link/Argus-Agentic-SOC-Platform](https://github.com/Sec-Link/Argus-Agentic-SOC-Platform) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
