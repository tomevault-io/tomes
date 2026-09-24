---
name: fix-tests
description: > Use when this capability is needed.
metadata:
  author: CopilotKit
---

# fix-tests

Fix failing tests in the repo from the brief.

1. Call `prepare_repository`, including `pr_number` when `kind` is `pr`.
2. Work on the returned branch; otherwise request `opentag/fix-tests-<short-id>`.
3. Find the test command: the brief, then `package.json` `test`/`ci`, then `pytest` or `go test ./...` if those files exist.
4. Run the command. Read the failure. Edit the smallest set of files that fixes it.
5. Re-run until exit 0 or you cannot fix it.
6. If green, commit locally and call `publish_changes`.
7. If red, do not call `publish_changes`. Return the log tail.

---
> Source: [CopilotKit/OpenTag](https://github.com/CopilotKit/OpenTag) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
