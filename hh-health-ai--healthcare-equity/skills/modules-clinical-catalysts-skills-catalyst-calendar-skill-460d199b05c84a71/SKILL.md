---
name: catalyst-calendar
description: > Use when this capability is needed.
metadata:
  author: hh-health-AI
---

# Catalyst Calendar

Build and refresh the clinical/regulatory catalyst calendar for a coverage universe, ranked for event-driven work.

## Workflow

1. Take the universe (tickers or watchlist) and horizon (default 6 months). For each name, sweep the Clinical Trials connector for late-stage trials: phase, status, primary completion date, primary endpoints, enrollment; note recent date changes. Add regulatory events from web research: PDUFA dates, scheduled FDA advisory committees (FDA AdCom calendar), CRL/response timelines, EMA CHMP meetings, EPAR Annex II conditional-approval obligation deadlines (confirmatory-study SOBs and annual renewals — dated, tradable), pending PAS-clocked supplements (device changes, shelf-life), and material PI/label supplements (see adcom-label's label-delta workflow); and major conference windows where the names present. Date the windows with the empirical review-timeline base rates in `${CLAUDE_PLUGIN_ROOT}/references/base-rates.md`.
2. Apply the SCR-02 prompt template (in `${CLAUDE_PLUGIN_ROOT}/skills/catalyst-calendar/references/prompts.md`): per catalyst — ticker, asset, event type · date window · base rate · prior data and success threshold · implied vs fundamental move · preliminary take — and close with the top 5 for deeper work.
3. Use TECH-06 (same file) for programmatic CT.gov API queries when the connector's search needs supplementing; use TECH-02 to emit Bloomberg BQL/terminal navigation for the user to run where terminal data (implied moves, event IDs) is needed — generate syntax, do not fabricate its output.
4. Merge in reimbursement catalysts from the cms-reimbursement plugin's rule-cycle calendar when installed, so the calendar covers clinical + FDA + CMS in one view.
5. Date discipline: sponsor-guided timing ("mid-2027 data") and registry primary-completion dates are different claims — show both and flag divergence; slippage is signal (see `${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`).
6. Rank by (a) proximity, (b) binary severity (share-price leverage), (c) thesis relevance. Hand the top events to readout-handicap or adcom-label for deep work, and to healthcare-equity `portfolio` (PORT-02) when events cluster.
7. End with an EVIDENCE BRIEF only for events analyzed in depth; the calendar itself is a dated table with sources.

---
> Source: [hh-health-AI/healthcare-equity](https://github.com/hh-health-AI/healthcare-equity) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
