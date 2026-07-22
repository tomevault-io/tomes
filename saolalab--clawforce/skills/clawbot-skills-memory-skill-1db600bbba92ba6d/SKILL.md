---
name: memory
description: Two-layer memory system with grep-based recall. Use when this capability is needed.
metadata:
  author: saolalab
---

# Memory

## Structure

- `.agents/memory/MEMORY.md` — Long-term facts (preferences, project context, relationships). Always loaded into your context.
- `.agents/memory/HISTORY.md` — Append-only event log. NOT loaded into context. Search it with grep.

## Search Past Events

```bash
grep -i "keyword" .agents/memory/HISTORY.md
```

Use the `exec` tool to run grep. Combine patterns: `grep -iE "meeting|deadline" .agents/memory/HISTORY.md`

## When to Update MEMORY.md

Write important facts immediately using `edit_file` or `write_file`:
- User preferences ("I prefer dark mode")
- Project context ("The API uses OAuth2")
- Relationships ("Alice is the project lead")

## Auto-consolidation

Old conversations are automatically summarized and appended to HISTORY.md when the session grows large. Long-term facts are extracted to MEMORY.md. You don't need to manage this.

---
> Source: [saolalab/clawforce](https://github.com/saolalab/clawforce) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
