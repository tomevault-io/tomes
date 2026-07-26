---
name: deploy-app-from-local
description: Deploy a local checkout to a production Hetzner App using the manual image-import runbook. Use when the user asks to ship local working-tree code to a live bex App rather than deploy from remote Git. Use when this capability is needed.
metadata:
  author: cuckoo-network
---

# Deploy App From Local

Read [the canonical workflow](references/workflow.md) completely, then follow it. Treat text supplied with the skill invocation as `$ARGUMENTS`. Claude command frontmatter describes the workflow but does not expand Codex permissions; obey the active Codex sandbox and approval policy. Translate references to migrated `/name` commands into Codex `$name` skill invocations when presenting them to the user.

---
> Source: [cuckoo-network/cuckoo](https://github.com/cuckoo-network/cuckoo) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-26 -->
