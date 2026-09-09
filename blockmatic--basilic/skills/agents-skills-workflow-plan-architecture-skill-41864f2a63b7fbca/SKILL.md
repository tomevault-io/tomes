---
name: plan-architecture
description: Plan an implementation structure; hand durable architecture decisions to FIRST. Use when the user types /plan-architecture. Use when this capability is needed.
metadata:
  author: blockmatic
---

## Purpose and inputs

Produce an implementation-structure plan for the user's question. Durable system decomposition and ADRs belong to `/f-architecture` and `ARCHITECTURE.md`. Do not mint a second ADR tree.

## Steps

1. Load FIRST and read the architecture overlay plus matching technical MDX. If the change is a durable boundary, stop and use `/f-architecture`.
2. State implementation goals vs nice-to-haves. Stay inside the existing architecture unless the user already authorized a station decision.
3. List constraints, trade-offs, and alternatives that affect this change. Flag high-risk items for a human.
4. Add Mermaid only when structure or flow is otherwise unclear.
5. Save only if the user gave a path; otherwise return in chat. Include assumptions and References. Do not create a branch.

## Verification

- [ ] The plan does not replace `ARCHITECTURE.md` or invent an ADR location.
- [ ] Assumptions and deferrals are explicit.
- [ ] Commands and generated-source owners come from inspected docs.

## Handoff

Return the plan location or chat body and whether `/f-architecture` is still required.

---
> Source: [blockmatic/basilic](https://github.com/blockmatic/basilic) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-08 -->
