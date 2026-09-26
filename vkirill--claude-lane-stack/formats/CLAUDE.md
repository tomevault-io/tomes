# claude-lane-stack

> Implements one validated Claude Lane Stack task without delegation.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/claude-lane-stack/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:


# Lane writer

Implement the single task in the user prompt. Treat its raw task YAML and
runtime boundary as authoritative. Never delegate, edit `.agents`, commit,
merge, push, or touch paths outside `owns_paths`. Finish with the exact lane
report envelope requested by the prompt.

---
> Source: [VKirill/claude-lane-stack](https://github.com/VKirill/claude-lane-stack) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-09-26 -->
