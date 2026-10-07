---
name: ada-coding
description: Implement and validate Swift, AdaScript, shader, and project-file changes in Ada projects. Use when this capability is needed.
metadata:
  author: AdaEngine
---

# Ada Coding

- Identify whether the project is AdaScript-only or SwiftPM-backed before selecting commands.
- Follow existing neighboring code, component registrations, plugins, and generated-source contracts.
- For AdaScript, use project diagnostics and the in-process AdaScript build. Do not invent Swift-only APIs.
- For `.ada` and `.gravity` source, use the Gravity LSP skill and editor Gravity tools for diagnostics, completion, hover, and definitions. Keep Swift source on SourceKit-LSP.
- For Swift, use the project package model and the narrowest applicable build or test.
- Preserve unrelated edits and report exact validation scope. Build output is not proof of runtime behavior when the change affects rendering or interaction.

---
> Source: [AdaEngine/Ada](https://github.com/AdaEngine/Ada) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
