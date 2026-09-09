# depthai-core

> DepthAI Core is the C++ SDK for Luxonis cameras, with Python bindings

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/depthai-core/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

DepthAI Core is the C++ SDK for Luxonis cameras, with Python bindings
through pybind11. It builds on Linux, macOS, and Windows (MSVC).

## Build & Test & Style
Follow instructions in the main README.md

## Layout
- `include/depthai/` — public headers
- `src/` — implementation
- `bindings/python/` — pybind11 bindings; a new public API needs a binding
- `examples/` — C++ and Python examples
- `shared/`, `3rdparty/` — submodules; do not edit
- `protos/` — schemas; run `ci/check_protobuf_consistency.sh` after a change

## Skills
A depthai specific review skill is avaialble at `.agents/skills/depthai-cpp-review/SKILL.md`

---
> Source: [luxonis/depthai-core](https://github.com/luxonis/depthai-core) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-09-08 -->
