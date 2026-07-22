---
name: daily-task-prep
description: | Use when this capability is needed.
metadata:
  author: beyonai
---

# Daily Task Prep

## Contract

This skill guarantees:
- Calendar/meetings for today are loaded with brain context per attendee
- Open threads from yesterday are surfaced
- Active tasks reviewed with priority ordering
- Prep briefing is actionable (not just informational)

## Phases

1. **Load calendar.** Check today's meetings. For each: load attendee brain pages, recent timeline, open threads.
2. **Check yesterday's threads.** Search brain for yesterday's timeline entries. Flag anything unresolved.
3. **Review active tasks.** Load `ops/tasks` from brain. Surface P0 and P1 items.
4. **Compile prep briefing.** Per-meeting context cards + open threads + task priorities.

## Output Format

```
Morning Prep — {date}
======================
Meetings today: {N}

## {Meeting 1 title} at {time}
Attendees: {names with brain context}
Context: {recent interactions, open threads}
Prep: {what to know before this meeting}

## Open Threads
- {thread from yesterday, with context}

## Tasks (P0-P1)
- {task with priority}
```

## Anti-Patterns

- Listing meetings without loading attendee context from brain
- Ignoring yesterday's unresolved threads
- Presenting tasks without priority ordering

---
> Source: [beyonai/ByClaw](https://github.com/beyonai/ByClaw) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
