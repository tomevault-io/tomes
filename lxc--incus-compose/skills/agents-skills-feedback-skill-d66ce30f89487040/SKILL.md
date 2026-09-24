---
name: feedback
description: Give feedback on teamwork after a task is done. Write a report to work/feedback/ in the main worktree. Use when this capability is needed.
metadata:
  author: lxc
---

Task done.

Give feedback on our teamwork (you and me). Report what happened in order; do
not explain why something landed or what changed your understanding.

Write that to the main worktree - the first entry of `git worktree list` at
work/feedback/$(date +%Y%m%d-%H%M%S).md, so every worktree collects in one
place. Create the directory if it is missing (terse for me only it is
gitignored).

The Stop hook archives the transcript to work/archive/<session-id>.jsonl every
turn, so it is already there. Name the session id in the write-up so the two
pair up.

---
> Source: [lxc/incus-compose](https://github.com/lxc/incus-compose) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
