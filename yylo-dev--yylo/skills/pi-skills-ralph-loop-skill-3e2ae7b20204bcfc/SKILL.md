---
name: ralph-loop
description: Execute exactly one explicitly assigned Kanban task to a validated queued commit. Use only when the user explicitly requests ralph-loop. Use when this capability is needed.
metadata:
  author: yylo-dev
---

Read [references/implement.md](references/implement.md) completely and follow it.

Stay within the assigned task. Do not select unrelated work, edit `tasks.md`, auto-tag releases, push, deploy, mutate production, or broaden scope because another issue is noticed. Record a bounded related Kanban follow-up when necessary.

Keep durable instructions concise and evidence-backed. Status belongs in the task response and runtime receipts, not `AGENTS.md`.

Controller checkpoints are best-effort local durability warnings after terminal metadata is durable. They never gate `yy pi`, `yy task`, `yy merge`, product commits, candidates, or releases.

## Complete assigned request

Treat the following as the complete user-assigned request. Preserve task references and directives literally; resolve them only through the normal agent workflow.

$ARGUMENTS

---
> Source: [yylo-dev/yylo](https://github.com/yylo-dev/yylo) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
