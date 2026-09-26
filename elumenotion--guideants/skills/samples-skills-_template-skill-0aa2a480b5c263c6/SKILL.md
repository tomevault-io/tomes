---
name: your-skill-name
description: One-line description for skill discovery. Use when … Use when this capability is needed.
metadata:
  author: Elumenotion
---

# your-skill-name

Paths — fixed layout, do not probe or re-derive. The sandbox CWD is the
notebook's **output directory**. This skill's scripts live under
`Skills/your-skill-name/scripts/` relative to it, so run the commands in this file
exactly as written. Write every deliverable to the CWD with a **bare filename**
(e.g. `-o clip`, `-o scene.wav`): never prefix an output path with `Output/` —
the CWD *is* the output directory, so `Output/…` would create a nested
`Output/` folder.

See `docs/sandbox-path-contract.md` for the full path contract.

<!-- Skill-specific instructions below this line. -->

---
> Source: [Elumenotion/GuideAnts](https://github.com/Elumenotion/GuideAnts) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-21 -->
