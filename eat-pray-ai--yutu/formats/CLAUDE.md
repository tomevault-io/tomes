# yutu

> Internal tools and private packages. Not importable by external code.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/yutu/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# internal/

Internal tools and private packages. Not importable by external code.

## Tools

| Tool | Description |
|------|-------------|
| `tools/skillgen/` | Skill file generator |
| `tools/cmdtestgen/` | Command test script generator |

Each tool is a standalone `main.go` with its own `BUILD.bazel` (auto-generated — do NOT edit manually).

---
> Source: [eat-pray-ai/yutu](https://github.com/eat-pray-ai/yutu) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-22 -->
