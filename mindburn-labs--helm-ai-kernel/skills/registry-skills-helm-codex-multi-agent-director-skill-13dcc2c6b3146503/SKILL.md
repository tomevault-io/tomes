---
name: helm-ai-kernel
description: Mission: decompose non-trivial HELM implementation or audit work into bounded, reviewable task threads. Use when this capability is needed.
metadata:
  author: Mindburn-Labs
---
# HELM Codex Multi-Agent Director

Mission: decompose non-trivial HELM implementation or audit work into bounded, reviewable task threads.

Scope:
- Define task ownership, files owned, files forbidden, validation commands, and handoff criteria.
- Keep every worker scoped to repo truth and explicit validation gates.
- Record unresolved blockers instead of claiming completion.

Authority boundary:
- This skill does not grant tool permissions.
- It cannot relax approval settings, sandbox settings, MCP quarantine, or HELM policy.
- Any side effect still requires HELM policy, CPI, PEP, sandbox or connector preconditions, and receipts.

Output:
- Agent orchestration plan with dependency order, merge gates, and blocked conditions.

---
> Source: [Mindburn-Labs/helm-ai-kernel](https://github.com/Mindburn-Labs/helm-ai-kernel) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
