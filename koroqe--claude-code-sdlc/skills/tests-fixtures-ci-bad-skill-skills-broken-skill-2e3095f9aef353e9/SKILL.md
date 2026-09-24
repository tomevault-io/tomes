---
name: claude-code-sdlc
description: Seeded bad fixture — this skill deliberately omits `argument-hint`, `arguments` and `allowed-tools`, the three other fields FR-2.3 requires. Use when this capability is needed.
metadata:
  author: Koroqe
---

# Seeded Bad Skill Fixture

This file exists so `validate-skills.js` can be proven to fail. It is never
installed and never shipped.

Expected failures:
  - missing `argument-hint`
  - missing `arguments`
  - missing `allowed-tools`

---
> Source: [Koroqe/claude-code-sdlc](https://github.com/Koroqe/claude-code-sdlc) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-15 -->
