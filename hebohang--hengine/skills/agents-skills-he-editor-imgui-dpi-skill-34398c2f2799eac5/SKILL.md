---
name: he-editor-imgui-dpi
description: Apply the repository's ImGui DPI-scaling conventions to layout, size, spacing, or column changes under Engine/Source/Editor. Use when this capability is needed.
metadata:
  author: hebohang
---

# Editor DPI rules

Use `Editor/ImGuiWrapper/ImGuiWrapper.h` helpers: `S(...)`, `SetColumnWidth`, `SetNextWindowSize`, `SetNextWindowSizeConstraints`, and `SameLine`.

- Do not add local `* uiScale` calculations in Editor code.
- Refresh cached column widths when `HasScaleChanged(...)` fires.
- Do not rescale values already in final pixel space, such as viewport/work-area coordinates.

Verify the changed panel follows these rules, then build `HEngineEditor` through `he-build-validate`.

---
> Source: [hebohang/HEngine](https://github.com/hebohang/HEngine) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-08 -->
