---
name: commission-research
description: End-to-end flow to quote and submit a paid research brief Use when this capability is needed.
metadata:
  author: ianalloway
---

# Commission research brief

## When to use

User wants a paid deliverable, mentions budget, topic, or checkout.

## Steps

1. Collect **topic**, **budget_cents**, **customer_email** (slot-fill across turns if needed).
2. Call `quote_brief` — share margin preview; decline if gate fails.
3. Ask for explicit confirmation.
4. Call `submit_brief` — return checkout URL; set expectations on payment → fulfillment → hosted link.
5. Offer `job_status` for tracking after submit.

## Rules

- Never claim paid until job status is `paid`.
- Do not skip quote before submit on non-trivial budgets.

---
> Source: [ianalloway/solvent-agent](https://github.com/ianalloway/solvent-agent) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
