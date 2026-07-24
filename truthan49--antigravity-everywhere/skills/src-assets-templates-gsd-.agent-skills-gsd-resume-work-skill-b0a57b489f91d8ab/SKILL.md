---
name: gsd-resume-work
description: Resume work from previous session with full context restoration Use when this capability is needed.
metadata:
  author: Truthan49
---


<objective>
Restore complete project context and resume work seamlessly from previous session.

Routes to the resume-project workflow which handles:

- STATE.md loading (or reconstruction if missing)
- Checkpoint detection (.continue-here files)
- Incomplete work detection (PLAN without SUMMARY)
- Status presentation
- Context-aware next action routing
  </objective>

<execution_context>
@.agent/get-shit-done/workflows/resume-project.md
</execution_context>

<process>
**Follow the resume-project workflow** from `@.agent/get-shit-done/workflows/resume-project.md`.

The workflow handles all resumption logic including:

1. Project existence verification
2. STATE.md loading or reconstruction
3. Checkpoint and incomplete work detection
4. Visual status presentation
5. Context-aware option offering (checks CONTEXT.md before suggesting plan vs discuss)
6. Routing to appropriate next command
7. Session continuity updates
   </process>

---
> Source: [Truthan49/Antigravity-Everywhere](https://github.com/Truthan49/Antigravity-Everywhere) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-15 -->
