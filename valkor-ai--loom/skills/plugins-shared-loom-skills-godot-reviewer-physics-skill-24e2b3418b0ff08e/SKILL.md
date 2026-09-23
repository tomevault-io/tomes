---
name: physics-review
description: | Use when this capability is needed.
metadata:
  author: valkor-ai
---

# Physics Review

Post-implementation reviewer for Godot physics code. Checks against known gotchas that LLMs consistently get wrong.

## When to trigger

After physics-related code is written or modified. Look for:
- Physics body nodes (StaticBody2D, RigidBody2D, CharacterBody2D, Area2D)
- Collision layer/mask assignments
- Physics callbacks (`body_entered`, `body_exited`, `area_entered`, `area_exited`)
- `_physics_process()` with velocity/damping logic
- Objects spawned near Area2D

## Review process

1. Read `gotchas.md`
2. Scan the implemented code against each gotcha
3. For each hit:
   - Cite the gotcha ID (e.g. G1)
   - Show the offending code
   - Provide the fix
4. If no hits, report clean
5. Optionally run `checklist.md` static checks for automated verification

When you need specific API details, delegate to the **godot-api** skill.

---
> Source: [valkor-ai/loom](https://github.com/valkor-ai/loom) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-19 -->
