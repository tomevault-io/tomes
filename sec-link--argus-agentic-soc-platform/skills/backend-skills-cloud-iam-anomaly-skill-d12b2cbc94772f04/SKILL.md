---
name: cloud-iam-anomaly-triage
description: Analyze suspicious cloud identity and access events, including role changes, new keys, unusual regions, and privilege escalation. Recommend evidence-preserving response actions. Use when this capability is needed.
metadata:
  author: Sec-Link
---
# Cloud IAM anomaly triage

Analyze suspicious cloud identity and access events, including role changes, new keys, unusual regions, and privilege escalation. Recommend evidence-preserving response actions.

Output requirements:
- Cite observed evidence from the ticket.
- Mark unknown values as unavailable.
- Return structured JSON fields when requested.
- Do not change ticket status or execute commands.

---
> Source: [Sec-Link/Argus-Agentic-SOC-Platform](https://github.com/Sec-Link/Argus-Agentic-SOC-Platform) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
