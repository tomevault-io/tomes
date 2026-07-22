---
name: caveman-stats
description: > Use when this capability is needed.
metadata:
  author: stevesolun
---

This skill is delivered by `hooks/caveman-stats.js` (read by `hooks/caveman-mode-tracker.js` on `/caveman-stats`). The model does not need to do anything when this skill fires — the hook returns `decision: "block"` with the formatted stats as the reason. The user sees the numbers immediately.

---
> Source: [stevesolun/ctx](https://github.com/stevesolun/ctx) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
