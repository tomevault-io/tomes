---
name: rule-cycle-calendar
description: > Use when this capability is needed.
metadata:
  author: hh-health-AI
---

# CMS Rule-Cycle Calendar

Maintain the CMS release rhythm as a standing catalyst feed for the coverage universe.

## Workflow

1. Start from the fixed annual calendar in the `${CLAUDE_PLUGIN_ROOT}/CLAUDE.md` (Advance Notice → Final Rate Notice → IPPS → PFS/OPPS/ASC → Stars → CLFS), then verify current-year dates and any off-cycle items (NCD reconsiderations, NTAP/TPT decisions, demonstration-model announcements) via web research on cms.gov. Never present last year's dates as this year's without checking.
2. For each upcoming release within the requested horizon (default 6 months), produce one row: event · expected window · names/sub-sectors exposed · the specific number to look for (e.g., benchmark growth rate, conversion factor, APC assignment) · prior-year outcome as the base rate · pre-committed reaction (what would make it thesis-relevant).
3. Tag each row with the evidence layer it will move (payor revenue, procedure economics, drug pricing) so `healthcare-equity` can merge it with clinical and FDA catalysts from the clinical-catalysts plugin into one calendar.
4. If the user wants this monitored rather than listed, offer to schedule the `rule-watcher` agent as a recurring scheduled task around the release windows (weekly during Feb/Apr/Jul/Oct/Nov; monthly otherwise).
5. End with the EVIDENCE BRIEF block only when a specific release has been analyzed; a pure calendar listing needs dates and exposure tags, not a brief.

---
> Source: [hh-health-AI/healthcare-equity](https://github.com/hh-health-AI/healthcare-equity) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
