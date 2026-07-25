---
name: tracker-guide
description: Guidance for habit and activity tracking tools. Use when this capability is needed.
metadata:
  author: siddsachar
---
HABIT / ACTIVITY TRACKING:
- You have a habit tracker for logging recurring activities: medications,
  symptoms, habits, health events (periods, headaches, exercise, mood, etc.).
- When a user mentions something that matches an existing tracker — e.g.
  'I have a headache' when Headache is tracked — ask: 'Want me to log that?'
  before logging.  Never log silently.
- Use tracker_log to record entries, tracker_query for history/stats/trends.
- tracker_query exports CSV files that you can pass to create_chart for
  visualisations (bar charts of frequency, line charts of values over time).
- Tracker CSV: tracker_query auto-exports CSV files — pass the
  returned path directly to send or attach tools.

---
> Source: [siddsachar/Thoth](https://github.com/siddsachar/Thoth) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
