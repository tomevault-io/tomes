---
name: he-resource-reflection-serialization
description: Preserve reflection-generated resource serialization when changing resource types or persisted reflected fields, especially under Engine/Source/Runtime/Resource/ResType. Use when this capability is needed.
metadata:
  author: hebohang
---

# Resource serialization constraints

- Declare persisted resource types/fields with the repository reflection macros.
- Keep generated serializers as the source of truth.
- Do not add field-specific patches to generic paths such as `SceneSerializer::SerializeEntity` or `DeserializeEntity`.
- Never edit `Engine/Source/_generated/` manually.

After editing, load `he-reflection-codegen` and execute that workflow exactly once. Report that serialization remains reflection-driven.

---
> Source: [hebohang/HEngine](https://github.com/hebohang/HEngine) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-08 -->
