---
name: gbt
description: Distill finished OpenClaw task logs into a reusable experience tree, guide covered tasks with cheaper executor models, and manage idle-time self-evolution approval via the bundled GBT plugin. Use when this capability is needed.
metadata:
  author: PeiranLi0930
---

# GBT

Use this plugin when OpenClaw is running with the bundled `gbt-skill` package and the user wants log-distilled reusable experience instead of repeated long-horizon planning.

## What GBT does

- After a task finishes, the plugin distills its tool log into reusable, non-task-specific macro nodes.
- When a new task matches existing experience with enough confidence, GBT switches to the configured cheaper executor model and injects macro-by-macro execution guidance.
- Failed covered runs are queued for self-evolve. After 10 minutes of OpenClaw idle time, the plugin asks for approval before attempting repair.
- Verified self-evolve repair uses GBT's built-in OpenClaw replay runner by default. The plugin can still override it with a custom replay command when needed.

## Operational rules

- This version does not implement the paper's safety gate system.
- Success and failure logs both become reusable experience nodes.
- Failed paths stay in the tree and are candidates for later self-evolve repair.
- Distillation and self-evolve use the same main model that produced the run unless the plugin config overrides `distillModel`.
- Recovery guidance and spine progress are tracked at runtime so the cheaper executor stays local to the current macro.
- The built-in replay runner silently replays the failed task in a fresh OpenClaw session, reads the real transcript, and only writes the repaired path back into the tree after verification succeeds.

## User-facing commands

- `/gbt status`
- `/gbt match <task>`
- `/gbt evolve approve`
- `/gbt evolve reject`

## Notes for the agent

- If GBT executor mode is active, follow the injected macro path instead of inventing a new long-horizon plan.
- Keep explanations of blockers concrete; they become self-evolve input later.
- If the user asks why self-evolve is paused, tell them it waits for explicit approval after the configured idle window.
- If the user asks why a repair is still not committed, check whether the built-in replay runner actually produced a verified successful trajectory, or whether the latest replay attempt is still failing verification.

---
> Source: [PeiranLi0930/Plugin-GBT](https://github.com/PeiranLi0930/Plugin-GBT) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
