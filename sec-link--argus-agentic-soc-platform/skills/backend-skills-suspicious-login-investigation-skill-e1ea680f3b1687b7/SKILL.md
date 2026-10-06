---
name: suspicious-login-investigation
description: Investigate unusual authentication activity using source IP, account, time, geolocation, MFA, and privilege context. Recommend validation steps and avoid changing ticket status. Use when this capability is needed.
metadata:
  author: Sec-Link
---
# Suspicious login investigation

Investigate unusual authentication activity using source IP, account, time, geolocation, MFA, and privilege context. Recommend validation steps and avoid changing ticket status.

Output requirements:
- Cite observed evidence from the ticket.
- Mark unknown values as unavailable.
- Return structured JSON fields when requested.
- Do not change ticket status or execute commands.

---
> Source: [Sec-Link/Argus-Agentic-SOC-Platform](https://github.com/Sec-Link/Argus-Agentic-SOC-Platform) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
