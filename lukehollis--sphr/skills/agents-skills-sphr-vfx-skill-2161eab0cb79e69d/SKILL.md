---
name: sphr-vfx
description: Add or fix SPHR visual effects, transitions, scene graph visibility, annotation effects, Spark recoloring, atmosphere changes, and interaction polish. Use when this capability is needed.
metadata:
  author: lukehollis
---

Use this for SPHR VFX and interaction polish.

## Runtime Surfaces

- `SparkSplatLayer` for Spark mesh opacity, recolor, reveal, and study modes.
- `SphrRuntime` for camera movement, atmosphere, event handling, and tour state.
- `AnnotationLayer` for annotation planes.
- `SceneGraphLayer` for GLB/model/lights visibility.
- `PanoramaLayer` and `IiifImageLayer` for non-splat visual layers.
- `app/globals.css` for HUD/tour/loading responsiveness.

## Implementation Rules

- Effects must serve tour comprehension or scene interaction. Avoid decorative-only clutter.
- Prefer layer-level APIs such as `setStudyMode`, `showOnly`, `show`, `setVisible`, or a new clear method.
- Keep frame-loop work bounded. Do not add per-frame allocations in hot paths.
- Use stable dimensions and responsive constraints for controls.
- Verify desktop and mobile screenshots; mobile controls must not overlap tour nav/copy.

## Common Effects

- Splat reveal: opacity/scale easing after Spark initialization.
- Study mode: recolor/opacity changes tied to tourpoint `extra`.
- Night/atmosphere: fog and tone exposure in `SphrRuntime.applyAtmosphere`.
- Annotation reveal: show only active annotation IDs for the current point.
- Model focus: scene graph `showOnly(point.models)`.

## Verification

```bash
npm run typecheck
npm run build
node .claude/scripts/project/verify-app.mjs --url http://localhost:3000 --screenshots
```

Final response should report the exact runtime layer changed, the user-facing effect, and verification outcome.

---
> Source: [lukehollis/sphr](https://github.com/lukehollis/sphr) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-26 -->
