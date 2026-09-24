---
name: meta-travel-planner
description: Use this meta-skill instead of answering directly when the user needs a trip plan, travel itinerary, business-trip schedule, or day-by-day travel brief that benefits from multi-skill orchestration across preference inference, weather, place search, constraint extraction, itinerary drafting, variants, and optional artifact guidance.
metadata:
  author: TokenRhythm
---

# Travel Planner (Meta-Skill)

Weather + POI/restaurant/transport search + constraints + a complete itinerary
with variants. The default answer is a complete travel plan; HTML export is an
optional handoff when the user explicitly asks for a file.

## Fallback

Manually call weather, multi-search-engine, summarize. If the user explicitly
asks for HTML export, ask the LLM to write a styled `travel-itinerary.html`
and `publish_artifact` it.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
