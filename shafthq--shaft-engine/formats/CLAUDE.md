# shaft-engine

> - Imported `AGENTS.md` is canonical (including binding `act-as-fable`);

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/shaft-engine/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# CLAUDE.md

@AGENTS.md

## Claude Adapter

- Imported `AGENTS.md` is canonical (including binding `act-as-fable`);
  do not restate it or append logs.
- Load one matching `.agents/skills/` bridge only when its trigger applies;
  native Graphify via `.claude/skills/graphify`.
- Keep plans and final responses proportional to the task; stop when the
  requested behavior is verified.

---
> Source: [ShaftHQ/SHAFT_ENGINE](https://github.com/ShaftHQ/SHAFT_ENGINE) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-24 -->
