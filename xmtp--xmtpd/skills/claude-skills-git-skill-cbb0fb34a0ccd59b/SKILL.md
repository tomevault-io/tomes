---
name: git
description: >- Use when this capability is needed.
metadata:
  author: xmtp
---

# Creating Branches and Pull Requests

## Branch Naming Convention

**Always** use `<github-username>/<branch-description>`:

- GitHub username: !`gh api user --jq '.login'`

```
<username>/payer-id-lru-cache
<username>/fix-fee-calculation
<username>/add-congestion-metrics
```

- Prefix is always the result of `gh api user --jq '.login'`
- Description is kebab-case, concise, imperative
- Never use `main`, a bare description, or any other prefix

---
> Source: [xmtp/xmtpd](https://github.com/xmtp/xmtpd) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
