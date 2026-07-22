---
name: dep-upgrade
description: Analyze a major version dependency upgrade: summarize breaking changes, assess project impact, and propose new features to adopt. Outputs a plan.md and executes the upgrade. Use when this capability is needed.
metadata:
  author: AtCoder-NoviSteps
---

Analyze and execute the major version upgrade for: $ARGUMENTS

1. **Analyze** — fetch the official migration guide via WebFetch; apply the checklist in [instructions.md](instructions.md)
2. **Generate plan** — create `docs/dev-notes/YYYY-MM-DD/{package}-upgrade/plan.md` with breaking changes, impact, and new features; **stop and ask for confirmation**
3. **Execute** — update `package.json`, run `pnpm install && pnpm lint && pnpm check && pnpm test:unit`; update the plan checklist when done

---
> Source: [AtCoder-NoviSteps/AtCoderNoviSteps](https://github.com/AtCoder-NoviSteps/AtCoderNoviSteps) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
