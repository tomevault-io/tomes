# cobalt

> Any time you are instructed to run `autoninja`, use

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/cobalt/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

Any time you are instructed to run `autoninja`, use
`agents/extensions/landmines/agent_autoninja` in its place.

If do not have access to "Code Search", then search locally using `rg` or
`fd-find`. Searching with "grep -r" or "find ." is too slow for chrome's large
source tree. If these commands are not installed, suggest to the user to
install. For Debian systems:

```
sudo apt-get install ripgrep fd-find
```

---
> Source: [youtube/cobalt](https://github.com/youtube/cobalt) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-24 -->
