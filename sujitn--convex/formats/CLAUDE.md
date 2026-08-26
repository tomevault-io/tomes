# convex

> The agent scaffolding (Claude memory, prompts, plans, internal reconciliation

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/convex/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Convex — agent context

The agent scaffolding (Claude memory, prompts, plans, internal reconciliation
notes) for this repo lives in a separate private repo and is mounted at `.ai/`
as a git submodule.

If `.ai/` is empty, you do not have access — that is expected for public clones.
If you do have access, run:

    git submodule update --init --recursive

The active agent context file is `.ai/CLAUDE.md`.

---
> Source: [sujitn/convex](https://github.com/sujitn/convex) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-08-26 -->
