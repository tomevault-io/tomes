---
name: portfolio
description: > Use when this capability is needed.
metadata:
  author: hh-health-AI
---

# Portfolio Construction & Risk

Book-level positioning, concentration, and monitoring. Prompts in `${CLAUDE_PLUGIN_ROOT}/skills/portfolio/references/prompts.md`.

## Route by need

| Need | Prompt |
|---|---|
| Quarterly sleeve positioning review | PORT-01 |
| Binary events clustering in the book | PORT-02 catalyst concentration & path dependence |
| Relative-value expression | PORT-03 pair trade construction |
| Before initiating/sizing a short | PORT-04 borrow, float & short interest |
| Quarterly 13F pass | SCR-06 institutional ownership delta |
| Hidden macro linkages | SCR-07 cross-sector correlation identifier |
| Automated filing surveillance | TECH-05 EDGAR agent configuration |

## Execution rules

1. Portfolio composition, factor exposures, borrow data, and 13F extracts come from the user (terminal/holdings systems) — request them; never invent positions or market data. 13F caveat applies (`${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`): 45-day lag, holdings only, directional not precise.
2. PORT-02 runs on the suite catalyst calendar: pull the dated events from clinical-catalysts (readouts, PDUFA, AdComs) and cms-reimbursement (rule cycle) for the book's names, then map calendar and factor concentration, worst/best P&L scenarios, hedges, and pre-trim vs hold/add per event.
3. Position sizing questions route to sell-discipline (SELL-03 sizing sanity check) — keep sizing discipline and book construction connected.
4. TECH-05's EDGAR monitoring is a standing surveillance recipe (Form 4 clusters, 8-K keywords — 'Complete Response Letter', 'voluntary recall', 'consent decree', executive departures — and 13F deltas); offer to run it as a recurring scheduled task and route hits into the relevant skill (earnings, thesis, sell-discipline).
5. Every recommendation shows the disconfirming case and ends with the confidence score (standing instructions).

---
> Source: [hh-health-AI/healthcare-equity](https://github.com/hh-health-AI/healthcare-equity) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
