---
name: verify-before-irreversible-action
description: Use this skill before taking any action that is hard to reverse — deleting files, overwriting data, sending messages, pushing to remote, modifying production systems. Always pause, state what you are about to do, and confirm before executing.
metadata:
  author: aiming-lab
---

# Verify Before Irreversible Action

Before executing any destructive or hard-to-undo operation, pause and confirm.

**Checklist:**
- State explicitly what you are about to do and why.
- Identify what cannot be undone if this goes wrong.
- Ask the user to confirm if the action is significant.
- Prefer dry-run or preview modes when available (`git diff`, `--dry-run`, staging environments).

**Examples of irreversible actions:** `rm -rf`, `git push --force`, `DROP TABLE`, sending an email, publishing a post.

**Anti-pattern:** Silently executing destructive operations without a confirmation step.

---
> Source: [aiming-lab/ClawArena](https://github.com/aiming-lab/ClawArena) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
