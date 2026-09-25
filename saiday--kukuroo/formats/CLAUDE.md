# kukuroo

> - Write PR titles, summaries, and descriptions in English.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/kukuroo/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Pull Requests

- Write PR titles, summaries, and descriptions in English.

# Releasing

`RELEASING.md` is the procedure, and it is not optional reading before a publish. Two
things it is easy to get wrong from the outside:

- A publish credential never goes in `~/.npmrc` or anywhere in the repo. `tools/npm-token.sh`
  is the only path to one, and `tools/` is outside `files` in `package.json` so it does
  not ship.
- The git tag names the commit the tarball was built from, which is not always `main`.

---
> Source: [saiday/kukuroo](https://github.com/saiday/kukuroo) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-09-24 -->
