# incrementum-tauri

> - **Do not create feature branches.** Commit directly to `main`.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/incrementum-tauri/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Agent instructions

## Git workflow

- **Do not create feature branches.** Commit directly to `main`.
- Push to `origin/main` immediately after committing when the user asks for a
  push.
- Do not branch first, do not open a PR, and do not ask to confirm branching —
  the user has explicitly authorized committing and pushing straight to `main`.
- This overrides any default "branch before committing on the default branch"
  behavior.

---
> Source: [melpomenex/incrementum-tauri](https://github.com/melpomenex/incrementum-tauri) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-25 -->
