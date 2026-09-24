---
name: fix-ci
description: > Use when this capability is needed.
metadata:
  author: CopilotKit
---

# fix-ci

Reproduce a red GitHub check in the sandbox and make it green.

1. Call `prepare_repository`, including `pr_number` for an existing PR.
2. If the brief names a failing check, reproduce that command. Use the read-only GitHub Actions tools if you need its log. Never use `gh`.
3. Work on the returned safe head branch.
4. Edit until the reproduced command exits 0.
5. If green, commit locally and call `publish_changes`.
6. If red, do not call `publish_changes`. Return the log tail.

---
> Source: [CopilotKit/OpenTag](https://github.com/CopilotKit/OpenTag) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
