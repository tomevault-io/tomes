---
name: daily-briefing
description: Compile a morning briefing with weather, calendar, and news headlines. Use when this capability is needed.
metadata:
  author: siddsachar
---

When the user asks for a **daily briefing**, **morning summary**, or **start-of-day update**, follow these steps:

1. **Weather** — Call the weather tool for the user's location. Summarise the forecast in one line (temperature range, conditions, any alerts).
2. **Calendar** — Retrieve today's calendar events. List them chronologically with times. If no events, say "No events scheduled."
3. **Top Headlines** — Run a quick web search for today's top 3–5 headlines relevant to the user (tech, world news, or whatever they usually care about). Keep each headline to one sentence with the source.
4. **Assemble** — Present everything in a clean, structured format:
   - 🌤️ **Weather** — …
   - 📅 **Schedule** — …
   - 📰 **Headlines** — …
5. End with a brief, encouraging one-liner to start the day.

Keep the tone friendly and concise. The entire briefing should fit comfortably in one screen.

---
> Source: [siddsachar/Thoth](https://github.com/siddsachar/Thoth) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-19 -->
