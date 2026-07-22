---
name: inspect
description: > Use when this capability is needed.
metadata:
  author: edmundmiller
---

# inspect Skill

Use inspect to review by **entity risk**, not line churn.

## Use when

- PR too large/noisy, need fast triage
- Need highest-risk entities first
- Need blast-radius/dependent-aware prioritization
- Need verdict: approvable vs careful review

## Core commands

```bash
inspect diff HEAD~1
inspect diff main..feature --min-risk high
inspect diff HEAD~1 --format json
inspect pr 42 --format json
inspect file src/path.rs --context
```

## MCP

`inspect-mcp` exposes triage/entity/group/file/stats/risk-map (+ pr/diff/review in current build).
Use for agent workflows when you need structured review objects.

## Workflow

1. Run `inspect diff <ref>`
2. Focus Critical/High first
3. Review by group (independent logical bundles)
4. Use verdict to choose review depth

## Reference

For full command + scoring + architecture details, read:

- `references/llms.txt`

---
> Source: [edmundmiller/dotfiles](https://github.com/edmundmiller/dotfiles) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
