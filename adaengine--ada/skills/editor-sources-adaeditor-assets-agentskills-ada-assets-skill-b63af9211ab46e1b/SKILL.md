---
name: ada-assets
description: Import, generate, configure, and connect image assets inside an Ada project. Use when this capability is needed.
metadata:
  author: AdaEngine
---

# Ada Assets

- Resolve the project's declared resource roots and reuse existing assets before generating duplicates.
- Use `editor.asset.list` to discover files under the project's `Assets` directory; it returns paths only and does not modify or import files.
- Keep generated or imported files under a resource root and return their project-relative path and `@res://` reference.
- Never overwrite an existing asset without explicit approval. Validate image data before saving it.
- When an asset is meant for a scene, connect it to the requested entity and component field rather than stopping after file creation.
- Rebuild or reload the owning scene and inspect a screenshot to verify scale, transparency, framing, and reference resolution.

---
> Source: [AdaEngine/Ada](https://github.com/AdaEngine/Ada) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
