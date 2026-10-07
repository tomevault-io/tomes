---
name: ada-ui-debugging
description: Inspect and debug AdaUI hierarchy, layout, focus, hit testing, and interaction behavior. Use when this capability is needed.
metadata:
  author: AdaEngine
---

# AdaUI Debugging

- Locate nodes by stable `accessibilityIdentifier` when possible; runtime IDs are session-local.
- Trace interaction failures through window, tree, layout, hit test, focus, and action state instead of guessing from source.
- Use layout diagnostics before changing frames or padding. Keep keyboard navigation and visible focus intact.
- Apply only deterministic UI actions, then re-read the node or tree.
- Capture and inspect the affected node after the fix, including compact-width behavior when the project targets iPadOS.

---
> Source: [AdaEngine/Ada](https://github.com/AdaEngine/Ada) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
