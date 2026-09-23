---
name: animation-review
description: | Use when this capability is needed.
metadata:
  author: valkor-ai
---

# Animation Review

Post-implementation reviewer for Godot animation code. Checks against known gotchas that LLMs consistently get wrong.

## When to trigger

After animation-related code is written or modified. Look for:
- Animation nodes (AnimationPlayer, AnimationTree, AnimatedSprite2D)
- AnimationTree state machine control (`travel()`, `start()`, `active`)
- SpriteFrames or Animation resource manipulation at runtime
- `callback_mode_process` settings
- Pool/spawn lifecycle involving animated entities
- Briefs or asset snapshots that require multi-frame `grid_sheet` runtime
  assets, dynamic-mode evidence, frame sequences, animated actors, or animated
  FX. Trigger even if the implementation contains no animation API; omitted
  expected animation is a finding.

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
