---
name: godot-api
description: | Use when this capability is needed.
metadata:
  author: valkor-ai
---

# Godot API Lookup

$ARGUMENTS

## Version detection

Docs are stored per Godot version under `doc_api/{version}/` and `doc_api_csharp/{version}/`
when the local API cache has been prepared.

Determine the version to use:
1. If the caller specifies a version (e.g. "4.4"), use that
2. If `project.godot` exists in the working directory, extract from `config/features`
3. Otherwise fall back to `latest`

Bootstrap if docs for the target version are missing. Resolve `tools/` relative
to this skill directory:
```bash
bash tools/ensure_doc_api.sh [version]
```

## How to answer

**Language selection:** `doc_api/{version}/` contains GDScript docs. `doc_api_csharp/{version}/` contains C# docs. Default to GDScript unless the caller asks about C#.

1. Read `doc_api/{version}/_common.md` — index of common classes
   - For C#: `doc_api_csharp/{version}/_common.md`
2. If the class is not there, read `_other.md` in the same directory
3. Read `doc_api/{version}/{ClassName}.md` for the full API
   - For C#: `doc_api_csharp/{version}/{ClassName}.md`
4. Return what the caller needs:
   - **Specific question** → relevant methods/signals with descriptions
   - **Full API request** → the entire class doc

**C# syntax reference:** `csharp.md` — C# Godot syntax, patterns, and recipes.

**GDScript syntax reference:** `gdscript.md` — GDScript language spec, type system, patterns.

---
> Source: [valkor-ai/loom](https://github.com/valkor-ai/loom) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-19 -->
