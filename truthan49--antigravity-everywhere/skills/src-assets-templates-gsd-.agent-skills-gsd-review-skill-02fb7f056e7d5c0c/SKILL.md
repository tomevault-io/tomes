---
name: gsd-review
description: Request cross-AI peer review of phase plans from external AI CLIs Use when this capability is needed.
metadata:
  author: Truthan49
---


<objective>
Invoke external AI CLIs (Gemini, the agent, Codex) to independently review phase plans.
Produces a structured REVIEWS.md with per-reviewer feedback that can be fed back into
planning via /gsd-plan-phase --reviews.

**Flow:** Detect CLIs → Build review prompt → Invoke each CLI → Collect responses → Write REVIEWS.md
</objective>

<execution_context>
@.agent/get-shit-done/workflows/review.md
</execution_context>

<context>
Phase number: extracted from $ARGUMENTS (required)

**Flags:**
- `--gemini` — Include Gemini CLI review
- `--claude` — Include the agent CLI review (uses separate session)
- `--codex` — Include Codex CLI review
- `--all` — Include all available CLIs
</context>

<process>
Execute the review workflow from @.agent/get-shit-done/workflows/review.md end-to-end.
</process>

---
> Source: [Truthan49/Antigravity-Everywhere](https://github.com/Truthan49/Antigravity-Everywhere) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-15 -->
