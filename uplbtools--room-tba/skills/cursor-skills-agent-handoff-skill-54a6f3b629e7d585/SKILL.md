---
name: agent-handoff
description: >- Use when this capability is needed.
metadata:
  author: uplbtools
---

# Agent handoff

Produce a **copy-paste handoff** the next agent can run without this chat.

## When

- Epic spans multiple PRs or sessions
- User delegates to another model/host
- Context window getting long — prefer fresh session + handoff over continuation

## Handoff template

```markdown
# [Project] — [Epic name]

**Repo:** org/repo · **Workspace:** absolute path
**Read first:** AGENTS.md, docs/agent-contract.md, relevant .cursor/skills/*

## North star
One sentence goal.

## Done (staging/main)
| PR | What |

## In flight
- Branch, PR URL, commit, what's left

## Next steps (ordered)
1. …
2. …

## Key files
- `path` — why

## Verify
- [ ] commands

## Constraints
- Branch flow, migrations, don't touch X

## Success criteria
- [ ] checkboxes
```

## Rules

- **Facts over narrative** — SHAs, PR numbers, file paths, migration filenames
- **Ordered next steps** — first action is unambiguous (merge PR X, run migration Y)
- **Scope limits** — what NOT to build
- **No slop** — handoff is for execution, not motivation
- Link issues (`#NNN`) with current AC state

## Room TBA defaults

- Flow: feature → `staging` → `main` only when user says ship
- `gh` / `vercel` on maintainer machine
- Tests in same PR as feature
- See [docs/agent-tooling.md](../../../docs/agent-tooling.md) for Caveman/Ponytail

---
> Source: [uplbtools/room-tba](https://github.com/uplbtools/room-tba) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
