---
name: plugins
description: Work on Node3D plugin packages and high-level integrations. Use for packages that compose core with addons, extend the Node3D runtime, expose browser-like or multimedia interfaces, integrate QML/audio/physics/other systems, and provide ergonomic APIs on top of lower-level Node3D primitives. Use when this capability is needed.
metadata:
  author: node-3d
---

# Plugins

Use this skill for high-level Node3D packages that make multiple lower-level pieces work together coherently.

## Workflow

1. Identify the lower-level packages the plugin composes: usually `@node-3d/core`, one or more native addons, and sometimes Three.js or QML assets.
2. Preserve the plugin role: make the composed system easy to use without hiding necessary low-level escape hatches.
3. Keep browser-mimicking APIs aligned with the core environment model rather than inventing incompatible globals.
4. Examples should show consumer-style composition through package imports.
5. Tests should cover the integration contract, not just isolated helpers.

## References

- Read [plugin-model.md](references/plugin-model.md) for package role, composition, and API expectations.
- Read [browser-like-apis.md](references/browser-like-apis.md) for browser/multimedia compatibility guidance.

---
> Source: [node-3d/node-3d](https://github.com/node-3d/node-3d) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
