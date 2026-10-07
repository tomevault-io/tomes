---
name: ma-bid-cycle
description: > Use when this capability is needed.
metadata:
  author: hh-health-AI
---

# Medicare Advantage Bid Cycle

Track the annual MA rate/bid cycle through each milestone and translate it into payor-name implications.

## Workflow

1. Anchor on the cycle stage (see the calendar in the `${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`): Advance Notice (Jan/Feb) → comments → Final Rate Notice (early Apr) → June bids → October Stars release → AEP (Oct–Dec) → January membership. State which stage the analysis sits in and what is still unknown.
2. Run the SUB-SVC-02 prompt in `${CLAUDE_PLUGIN_ROOT}/skills/ma-bid-cycle/references/prompts.md`: rate-notice components → industry benefit-design response → bid aggressiveness by issuer → preliminary AEP indicators → final AEP results → next-year implications by name.
3. Decompose the rate components explicitly: effective growth rate, risk-model revision phase-in (V28), Star Ratings/quality-bonus changes, normalization factor — and map each to issuer-level revenue PMPM. Pull the notice itself from cms.gov; use KFF and issuer commentary for triangulation.
4. Connect Stars to the two-year-forward bonus revenue and rebate capacity; note contract-level concentration (a single large contract slipping below 4 stars is a name-specific event).
5. Distinguish rate evidence from utilization evidence: the rate cycle sets revenue; the MLR bridge (in `healthcare-equity` earnings) sets cost. Do not let a favorable rate notice masquerade as margin recovery — per the managed-care scenario row, the discriminator is **reserve-normalized current-year MCR**.
6. End with the EVIDENCE BRIEF block; feed dated milestones to the catalyst calendar and model deltas to `healthcare-equity`.

---
> Source: [hh-health-AI/healthcare-equity](https://github.com/hh-health-AI/healthcare-equity) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
