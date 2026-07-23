---
name: fix-ci
description: | Use when this capability is needed.
metadata:
  author: gadget-inc
---

Use the `gh` CLI to identify the most recent build for the current branch. Inspect which jobs failed, and then download and carefully analyze the logs for each failed job. Identify each failed test case or lint script or whatever, and create a todo for each. Then, fix each failure, validating each one as you go. Report back to the user with what was fixed and how.

---
> Source: [gadget-inc/silo](https://github.com/gadget-inc/silo) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
