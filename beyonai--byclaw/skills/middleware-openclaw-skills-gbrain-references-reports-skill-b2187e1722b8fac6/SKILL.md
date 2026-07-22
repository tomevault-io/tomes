---
name: reports
description: | Use when this capability is needed.
metadata:
  author: beyonai
---

# Reports Skill

## Contract

This skill guarantees:
- Reports saved with timestamped filenames and frontmatter
- Keyword routing: query → report category mapping
- Latest report loadable by category name
- Reports are searchable via gbrain search/query

## Phases

1. **Save report.** Write to `reports/{category}/{YYYY-MM-DD-HHMM}.md` with frontmatter:
   ```yaml
   ---
   title: {report title}
   type: report
   category: {category name}
   date: {YYYY-MM-DD}
   time: {HH:MM PT}
   ---
   ```
2. **Load latest.** Given a category, find the most recent report file.
3. **Keyword routing.** Map common queries to report categories:
   - "email" / "inbox" → ea-inbox-sweep
   - "social" / "mentions" → social-mentions
   - "briefing" / "morning" → morning-briefing
   - "meeting" → meeting-sync
   - Custom mappings configurable

## Output Format

Saved: `reports/{category}/{YYYY-MM-DD-HHMM}.md`
Loaded: full report content with metadata.

## Anti-Patterns

- Saving reports without frontmatter (makes them unsearchable)
- Using inconsistent category names across runs
- Loading all reports when only the latest is needed
- Not routing by keyword (forcing exact category name)

---
> Source: [beyonai/ByClaw](https://github.com/beyonai/ByClaw) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
