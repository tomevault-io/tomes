---
name: guideants
description: Deliberately missing the required 'name' field to test import rejection. Use when this capability is needed.
metadata:
  author: Elumenotion
---

# Invalid skill fixture

This SKILL.md is intentionally invalid. `SkillFrontmatter.Parse` requires both
`name` and `description`; this file omits `name` to verify the importer
rejects it explicitly instead of silently accepting a partial skill.

---
> Source: [Elumenotion/GuideAnts](https://github.com/Elumenotion/GuideAnts) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
