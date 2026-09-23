---
name: libero-fix-loop
description: Run the baseline-free LIBERO-Pro Fix Loop: inspect one initial observed scene, generate task-level code, debug failures on seeds 51–65 using traces and keyframes, validate on seeds 1–50, and promote reusable patterns. Use when this capability is needed.
metadata:
  author: NVlabs
---

# LIBERO Fix Loop

Use this skill for Experiment 1. Start with [INSTRUCTIONS.md](INSTRUCTIONS.md).

## Run Order

1. Follow [main-agent-prompt.md](main-agent-prompt.md) as coordinator.
2. Fill [subagent-prompt.md](subagent-prompt.md) once per task.
3. Each worker follows [skills/task-exploration.md](skills/task-exploration.md), generates its own initial code, then uses the original failure-by-failure debug loop.
4. Use [clean-task-slate.md](clean-task-slate.md) before reruns.
5. Promote Stage 1-supported patterns into [../skills/](../skills/) and record each update with `scripts/libero/record_skill_promotion.py` before dispatching the next Stage 1 task. Held-out outcomes never drive skill edits.

No external baseline code or baseline output directory is used.

---
> Source: [NVlabs/ASPIRE](https://github.com/NVlabs/ASPIRE) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
