---
name: module-conventions-generator
description: Generate or refactor modules, jobs, cache layers, gateways, and mappers to match ecommerce-store-api conventions. Use when creating new implementation artifacts so structure, naming, layering, and testing stay consistent automatically. Use when this capability is needed.
metadata:
  author: raouf-b-dev
---

# Purpose

Apply canonical repository conventions during generation with minimal drift.

# Workflow

1. Load and apply [docs/ai/CONVENTIONS.md](../../../docs/ai/CONVENTIONS.md), especially sections 1 through 8.
2. Identify artifact type (module, use case, gateway, scheduler, process, cache/repository, mapper).
3. Generate files in correct layer paths and naming conventions.
4. Enforce ACL and thin-controller boundaries.
5. Add or update tests using section 7 rules.
6. Produce verification and handoff evidence using section 9 rules.

# Inputs

- Requested feature/change.
- [docs/ai/CONVENTIONS.md](../../../docs/ai/CONVENTIONS.md)
- [AGENT.md](../../../AGENT.md)

# Outputs

- Convention-compliant implementation changes.
- Verification summary with tests and residual risks.

# Failure and Escalation

Escalate if requested behavior conflicts with architecture invariants or required safety gates.

---
> Source: [raouf-b-dev/ecommerce-store-api](https://github.com/raouf-b-dev/ecommerce-store-api) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
