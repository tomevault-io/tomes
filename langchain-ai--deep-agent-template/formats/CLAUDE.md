# deep-agent-template

> All agents are defined in `src/deep_agent/graph.py`.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/deep-agent-template/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Agents

All agents are defined in `src/deep_agent/graph.py`.

## Conventions

- Prefer async-native code wherever possible for performance. Tools, tests, and any new I/O should use async.
- New tools should be low-dependency and safe to run on a remote server.
- This deploys in a web server. Avoid calls to actual file system.

---
> Source: [langchain-ai/deep-agent-template](https://github.com/langchain-ai/deep-agent-template) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-04-27 -->
