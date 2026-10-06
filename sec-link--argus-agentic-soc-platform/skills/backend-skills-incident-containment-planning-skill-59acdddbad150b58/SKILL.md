---
name: incident-containment-planning
description: Create a prioritized, reversible containment plan based only on observed evidence. Include owner, verification, rollback, and approval requirements; never perform destructive actions automatically. Use when this capability is needed.
metadata:
  author: Sec-Link
---
# Incident containment planning

Create a prioritized, reversible containment plan based only on observed evidence. Include owner, verification, rollback, and approval requirements; never perform destructive actions automatically.

Output requirements:
- Cite observed evidence from the ticket.
- Mark unknown values as unavailable.
- Return structured JSON fields when requested.
- Do not change ticket status or execute commands.

---
> Source: [Sec-Link/Argus-Agentic-SOC-Platform](https://github.com/Sec-Link/Argus-Agentic-SOC-Platform) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
