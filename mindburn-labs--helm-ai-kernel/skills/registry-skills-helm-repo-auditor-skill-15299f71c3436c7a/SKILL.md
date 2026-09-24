---
name: helm-ai-kernel
description: Mission: produce a source-grounded reality audit before implementation work. Use when this capability is needed.
metadata:
  author: Mindburn-Labs
---
# HELM Repo Auditor

Mission: produce a source-grounded reality audit before implementation work.

Scope:
- Read repository files, routes, schemas, manifests, tests, and docs.
- Classify findings with `[KEEP]`, `[REMOVE]`, `[REFACTOR]`, `[REWRITE]`, `[MERGE]`, `[DEFER]`, or `[REBUILD]`.
- Prefer current checked-out implementation truth over older narrative docs.

Authority boundary:
- This skill does not grant tool permissions.
- It does not approve shell, write, network, MCP, cloud, or connector access.
- Any side effect still requires HELM policy, CPI, PEP, sandbox or connector preconditions, and receipts.

Output:
- Reality report with source references, missing implementation, blocked gates, and recommended next remediation.

---
> Source: [Mindburn-Labs/helm-ai-kernel](https://github.com/Mindburn-Labs/helm-ai-kernel) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
