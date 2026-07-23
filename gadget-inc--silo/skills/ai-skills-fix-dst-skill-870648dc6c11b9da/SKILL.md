---
name: fix-dst
description: | Use when this capability is needed.
metadata:
  author: gadget-inc
---

Use the `gh` CLI to identify the most recent build for the current branch of the `simulation-testing` github actions workflow. Retrieve the action logs and review the list of failed seeds at the end of the log. Identify the failed scenarios and reproduce the failure locally -- it should be fully deterministic and fail in the same way locally as it did in CI. Create a todo for each seed, and debug. Then, fix each failure, validating each one as you go. Report back to the user with what was fixed and how.

---
> Source: [gadget-inc/silo](https://github.com/gadget-inc/silo) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
