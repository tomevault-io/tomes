---
name: landing-the-plane
description: Completes work sessions by running quality gates, syncing bd, pushing to remote, and handing off. Use when ending a work session, landing the plane, session completion, or when the user asks to wrap up or finish work. Use when this capability is needed.
metadata:
  author: radiantlogicinc
---

# Landing the Plane (Session Completion)

When ending a work session, complete ALL steps below. Work is NOT complete until `git push` succeeds.

## Mandatory workflow

1. **File issues for remaining work** – Create issues (e.g. via `bd create`) for anything that needs follow-up.
2. **Run quality gates** (if code changed) – Tests, linters, builds.
3. **Update issue status** – Close finished work, update in-progress items (`bd close <id>`, `bd update <id> --status ...`).
4. **PUSH TO REMOTE** – Mandatory:
   ```bash
   git pull --rebase
   bd sync
   git push
   git status   # MUST show "up to date with origin"
   ```
5. **Clean up** – Clear stashes, prune remote branches.
6. **Verify** – All changes committed AND pushed.
7. **Hand off** – Provide context for next session.

## Critical rules

- Activate the local Python environment before running scripts/tests.
- Work is NOT complete until `git push` succeeds.
- NEVER stop before pushing – that leaves work stranded locally.
- NEVER say "ready to push when you are" – you must push.
- If push fails, resolve and retry until it succeeds.

---
> Source: [radiantlogicinc/fastworkflow](https://github.com/radiantlogicinc/fastworkflow) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
