---
name: ada-visual-verification
description: Verify scene, rendering, and AdaUI changes with live inspection and screenshots. Use when this capability is needed.
metadata:
  author: AdaEngine
---

# Ada Visual Verification

Use this after any change whose success is visible.

1. Build and launch the exact project and scene in scope.
2. Use `editor.scene.get` to confirm the open scene revision and hierarchy before launch. Locate the runtime window or viewport using its accessibility identifier or inspected UI tree.
3. Capture the smallest screenshot that proves the result; use a full render capture for game output and a node capture for AdaUI or editor layout.
4. Inspect the image and relevant diagnostics. If the result is wrong, fix it and repeat the same capture.

Never treat compilation, a saved PNG path, or a screenshot without visible rendered content as runtime proof.

---
> Source: [AdaEngine/Ada](https://github.com/AdaEngine/Ada) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
