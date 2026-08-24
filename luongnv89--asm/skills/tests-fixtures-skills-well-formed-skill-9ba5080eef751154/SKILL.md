---
name: well-formed
description: Review pull request diffs for code smells, style issues, and safety problems before merging. Use when this capability is needed.
metadata:
  author: luongnv89
---

# Well-formed corpus skill

## When to Use

- When the user asks to "review this PR" or "check the diff"
- Before merging any change larger than 10 lines

## Prerequisites

- A git repository with the target branch checked out
- Read access to the files being reviewed

## Instructions

1. Run `git diff main...HEAD` to list files
2. Read each file and check for common smells
3. Emit a markdown report summarising findings

## Example

```bash
$ asm eval ./well-formed
Overall score: 95/100
```

## Acceptance Criteria

- Produces a markdown report with sections per file
- Flags any use of `eval()` or `exec` as dangerous
- Does not modify the working tree

## Edge cases

- Empty diffs: emit a short "no changes" note
- Binary files: skip and mention the filename in the report

## Safety

See `references/safety.md` for error handling rules.
Always confirm before writing. Never run destructive commands without a dry-run.

---
> Source: [luongnv89/asm](https://github.com/luongnv89/asm) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
