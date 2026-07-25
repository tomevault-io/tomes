---
name: dotfiles-agent-workflow
description: Use this skill to apply the canonical risk-gated dotfiles workflow when work is broad, autonomous, high-risk, or multi-session; when the user tags AGENT_WORKFLOW.md; or when repeated agent friction needs durable guidance.
metadata:
  author: edmundmiller
---

# Dotfiles agent workflow

Read `AGENT_WORKFLOW.md`; it is the source of truth.

## Apply

1. Route through root and nearest nested `AGENTS.md`.
2. For qualifying work, copy `.agents/worklogs/TEMPLATE.md` and record the outcome, stopping condition, risks, and verification surfaces.
3. Before high-risk implementation, run the plan gate. Record an exact blocker; never silently skip it.
4. Follow the implementation and documentation sections. For qualifying work, keep the worklog current with decisions and evidence.
5. For qualifying work, run the full landing gate in `AGENT_WORKFLOW.md`. Otherwise, run focused checks and the landing steps required by root `AGENTS.md`.

---
> Source: [edmundmiller/dotfiles](https://github.com/edmundmiller/dotfiles) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
