---
name: clai
description: Inspect the local repository and summarize useful debugging signals for skill loading experiments. Use when this capability is needed.
metadata:
  author: baalimago
---

# Local skill debug helper

Investigate the repository for information relevant to `$focus`.

## Procedure

1. Identify the files and directories most relevant to the requested focus.
2. Read only the smallest necessary slices of code or docs.
3. Summarize:
   - what was discovered
   - which files matter
   - what to run next for end-to-end debugging

## Output

Return a concise debugging note with exact file paths and commands when helpful.

---
> Source: [baalimago/clai](https://github.com/baalimago/clai) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
