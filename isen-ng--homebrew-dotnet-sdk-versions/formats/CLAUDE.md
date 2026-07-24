# homebrew-dotnet-sdk-versions

> - This project uses a master `.aiskills/` directory.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/homebrew-dotnet-sdk-versions/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

## AI Skills Symlink Architecture
- This project uses a master `.aiskills/` directory.
- All AI agents (.claude, .windsurf, .cursor, .agents, .factory) MUST have symlinks to these skills.
- If a PR adds a new skill to `.aiskills/`, the contributor MUST run `./sym-link-aiskills.sh`.
- **Reviewer Task**: If you see new files in `.aiskills/` but no corresponding symlink updates in the agent folders, flag this as a required change.

---
> Source: [isen-ng/homebrew-dotnet-sdk-versions](https://github.com/isen-ng/homebrew-dotnet-sdk-versions) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-24 -->
