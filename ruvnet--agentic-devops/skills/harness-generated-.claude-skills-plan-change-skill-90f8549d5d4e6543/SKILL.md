---
name: plan-change
description: Plan changes to this repository using its domain CLI, MCP boundaries, and harness validation evidence. Use when this capability is needed.
metadata:
  author: ruvnet
---

Identify the requested outcome, affected domain interfaces and validation commands in the root README. Check repository.json for actual CLI routes. Separate domain behavior from harness mechanics: passing kernel or host tests does not validate the domain implementation.

Include authorization, input bounds, provenance and rollback where the requested change crosses a trust boundary. Preserve existing user authorization. When implementation is requested, continue through implementation and the relevant domain tests after planning.

---
> Source: [ruvnet/agentic-devops](https://github.com/ruvnet/agentic-devops) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
