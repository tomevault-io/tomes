---
name: run-in-sandbox
description: When you call `execute_bash` function, it runs in a sandboxed environment. You Use when this capability is needed.
metadata:
  author: breadboard-ai
---

# The sandbox

When you call `execute_bash` function, it runs in a sandboxed environment. You
have acess to most bash commands. The `PATH` is configured to give you access to
`node` and `python3`.

Even though you can use heredoc to write and `cat` to read files, prefer the
built-in file functions, if they available.

---
> Source: [breadboard-ai/breadboard](https://github.com/breadboard-ai/breadboard) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
