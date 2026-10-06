---
name: ransomware-response
description: Triage ransomware indicators such as mass file changes, encryption processes, ransom notes, and lateral movement. Prioritize isolation, evidence preservation, recovery coordination, and safe next tasks. Use when this capability is needed.
metadata:
  author: Sec-Link
---
# Ransomware response

Triage ransomware indicators such as mass file changes, encryption processes, ransom notes, and lateral movement. Prioritize isolation, evidence preservation, recovery coordination, and safe next tasks.

Output requirements:
- Cite observed evidence from the ticket.
- Mark unknown values as unavailable.
- Return structured JSON fields when requested.
- Do not change ticket status or execute commands.

---
> Source: [Sec-Link/Argus-Agentic-SOC-Platform](https://github.com/Sec-Link/Argus-Agentic-SOC-Platform) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
