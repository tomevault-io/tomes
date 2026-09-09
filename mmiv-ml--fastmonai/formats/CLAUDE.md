# fastmonai

> - Treat `nbs/*.ipynb` as the source of truth for nbdev-exported package code.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/fastmonai/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Repository Guidelines

## nbdev workflow

- Treat `nbs/*.ipynb` as the source of truth for nbdev-exported package code.
- Do not edit generated `fastMONAI/*.py` modules directly.
- After changing library notebooks, run `nbdev_prepare` from the repository root to regenerate modules and run checks.

---
> Source: [MMIV-ML/fastMONAI](https://github.com/MMIV-ML/fastMONAI) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-09-09 -->
