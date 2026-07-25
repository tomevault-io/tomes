# training-extensions

> - Use project skills from `.claude/skills/` when the task matches them; they are

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/training-extensions/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

@AGENTS.md

## Claude Code Adapter

- Use project skills from `.claude/skills/` when the task matches them; they are
  symlink adapters into the canonical `skills/<bucket>/<name>` directories.
- Author and edit skills under `skills/`, then run
  `python3 .github/scripts/skills/agent_skills.py sync` to refresh the adapters.

---
> Source: [open-edge-platform/training_extensions](https://github.com/open-edge-platform/training_extensions) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-25 -->
