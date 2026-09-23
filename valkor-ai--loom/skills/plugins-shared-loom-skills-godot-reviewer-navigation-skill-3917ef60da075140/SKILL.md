---
name: navigation-review
description: | Use when this capability is needed.
metadata:
  author: valkor-ai
---

# Navigation Review

Post-implementation reviewer for Godot navigation code. Checks against known gotchas that LLMs consistently get wrong.

## When to trigger

After navigation-related code is written or modified. Look for:
- Navigation nodes (NavigationAgent2D/3D, NavigationRegion2D/3D, NavigationLink2D/3D, NavigationObstacle2D/3D)
- `target_position` / `TargetPosition` assignment
- `avoidance_enabled`, `velocity_computed`, `safe_velocity`
- `bake_navigation_polygon()`, `navigation_layers`
- `is_navigation_finished()`, `get_next_path_position()`

## Review process

1. Read `gotchas.md`
2. Scan the implemented code against each gotcha
3. For each hit: cite gotcha ID, show offending code, provide fix
4. If no hits, report clean
5. Optionally run `checklist.md` static checks for automated verification

When you need specific API details, delegate to the **godot-api** skill.

---
> Source: [valkor-ai/loom](https://github.com/valkor-ai/loom) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-19 -->
