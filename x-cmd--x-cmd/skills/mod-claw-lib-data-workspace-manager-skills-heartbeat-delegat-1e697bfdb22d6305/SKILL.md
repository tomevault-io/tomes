---
name: claw-heartbeat-delegation
description: | Use when this capability is needed.
metadata:
  author: x-cmd
---

# Heartbeat Delegation

## Overview

`HEARTBEAT.md` is your delegation form to the heartbeat agent. Write clearly what needs to be done and when. The heartbeat agent reads and processes it during idle periods.

- **One-time tasks** (`## In Progress`): After execution, the heartbeat agent marks them completed or removes them.
- **Recurring tasks** (`## Recurring`): After execution, the heartbeat agent records the run in its own `memory/state.yml` but keeps the task in `HEARTBEAT.md` for future runs.

> **Important**: Do NOT execute items in `HEARTBEAT.md` yourself during the current session. Your role is to read it for awareness of pending follow-ups, but execution is the heartbeat agent's responsibility. If a user asks about a `HEARTBEAT.md` item, briefly summarize its status; only perform the action if the user explicitly says "do it now" or similar.

## Format Reference

### One-time follow-up

Write under `## In Progress`:

```markdown
- **Follow-up**: `<task-id>`
  - **Due**: YYYY-MM-DD HH:MM
  - **Task**: <description>
```

### Recurring check

Write under `## Recurring`:

```markdown
- **Recurring**: `<task-id>`
  - **Frequency**: <hourly | daily | weekly>
  - **Task**: <description>
```

### Background Job record

When you create a background job via `x agent run`, also record it in `HEARTBEAT.md` under `## In Progress`:

```markdown
- **Background Job**: `<job-id>`
  - **Display Name**: <friendly name>
  - **IM**: <im>
  - **Chat ID**: <chatid>
  - **Task**: <brief description>
  - **Created**: <timestamp>
  - **Check command**: `x agent job status --job-id <job-id> --llms`
  - **Notify command**: `x claw agentrequest <im> <chatid> '<summary>'`
```

## Checking Completion

The heartbeat agent periodically checks active background jobs:

1. Run: `x agent job status --job-id "<id>" --llms`
2. Read the output to determine if the job is done, failed, or still running
3. When done, report the summary to the user directly via stdout in the next session, or send a notification to the relevant platform if appropriate

---
> Source: [x-cmd/x-cmd](https://github.com/x-cmd/x-cmd) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
