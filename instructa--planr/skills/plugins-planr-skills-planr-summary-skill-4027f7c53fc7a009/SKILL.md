---
name: planr-summary
description: Summarize a Planr scope after work, review, or status inspection. Use when the user wants what changed, why, what works now, verification evidence, and what remains. Use when this capability is needed.
metadata:
  author: instructa
---

# Planr Summary

Build the summary from current Planr evidence:

```bash
planr map show --json
planr plan audit <plan-id> --json
planr trace item <item-id>
planr log list --item <item-id>
```

## Output

Include:

- scope;
- what changed;
- why;
- what works now;
- verification commands and results;
- open blockers or unverified items;
- any explicitly required material ReviewGate state when the summary is plan-scoped;
- next recommended Planr command.

If completion is not proven, say so directly and recommend `planr-status` or `planr-work`; recommend `planr-review` only when an explicit material ReviewGate is open.

---
> Source: [instructa/planr](https://github.com/instructa/planr) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-17 -->
