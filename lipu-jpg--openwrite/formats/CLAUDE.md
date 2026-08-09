# openwrite

> - Use `~/my_novel` as the only project for manual, live-server, and browser QA.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/openwrite/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# OpenWrite workspace instructions

- Use `~/my_novel` as the only project for manual, live-server, and browser QA.
- Do not create or open temporary novel projects for manual QA. Extend `~/my_novel`
  with any fixtures needed to exercise new features.
- Automated pytest cases may use isolated temporary directories, but must inject an
  isolated `ProjectRegistry` and must never write those paths to the user's default
  recent-project registry.
- The OpenWrite framework repository and `reference/my_novel` are not active novel
  projects.

---
> Source: [LiPu-jpg/Openwrite](https://github.com/LiPu-jpg/Openwrite) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-08-09 -->
