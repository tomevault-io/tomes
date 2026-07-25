---
name: avoid-scope-creep
description: Common mistake — doing unrequested work (refactoring, adding extra features, cleaning up style) when the user asked for a specific, targeted change. Only change what was explicitly asked. Use when this capability is needed.
metadata:
  author: aiming-lab
---

# Avoid Scope Creep

**Mistake pattern:** User asks to fix a specific bug → you also refactor the function, rename variables, add docstrings, and restructure the file → harder to review, introduces new risk.

**Rule:** Only change what was asked. If you notice other issues while working, mention them as a note rather than silently fixing them.

**Exception:** If a requested change is impossible without fixing a directly blocking dependency, fix the minimum required dependency and explain why.

**Anti-pattern:** `while I'm here, I also improved...` without being asked.

---
> Source: [aiming-lab/ClawArena](https://github.com/aiming-lab/ClawArena) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
