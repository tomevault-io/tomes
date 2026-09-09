---
name: gh
description: Diagnose GitHub CLI hiccups caused by Codex sandbox constraints; not a general GitHub workflow. Use when this capability is needed.
metadata:
  author: zoltanmaric
---

Use this skill only for GitHub hiccups. This is the second time Codex has hiccupped on `gh auth status`: an apparent invalid login is really a sandbox constraint. Retry the command with escalated sandbox permissions before diagnosing an authentication problem.

---
> Source: [zoltanmaric/coppersushi](https://github.com/zoltanmaric/coppersushi) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-07 -->
