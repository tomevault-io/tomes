---
name: drug-pricing-ira
description: > Use when this capability is needed.
metadata:
  author: hh-health-AI
---

# Drug Pricing & IRA Exposure

Map a branded pharma/biotech name's exposure to US drug-pricing reform, asset by asset.

## Workflow

1. Build the asset inventory: each marketed product with US revenue, molecule type (small molecule vs biologic), FDA approval date, and Medicare (Part B vs Part D) revenue mix from filings.
2. Run the ESG-03 prompt in `${CLAUDE_PLUGIN_ROOT}/skills/drug-pricing-ira/references/prompts.md`: asset-by-asset negotiation exposure (9-year small-molecule / 13-year biologic thresholds) → Part D redesign impact → 340B exposure → inflation rebate → mitigations → net thesis impact vs consensus.
3. Ground the selection mechanics in primary sources via web research: CMS's published selected-drug lists and negotiated "maximum fair prices", the annual selection calendar, and eligibility rules (spend ranking, small-biotech and orphan exceptions). Time-stamp which negotiation cycle each claim refers to.
4. Model the *behavioral* responses, not just the price cut: launch-timing and indication-sequencing incentives ("small-molecule penalty"), net-price convergence with existing rebates (the negotiated price hit is measured against net, not list), and Part D redesign's reallocation of catastrophic-phase liability to plans and manufacturers.
5. Separate federal-policy evidence (this skill) from Medicare coverage evidence (coverage-check) and from state/PBM dynamics (label separately if material).
6. End with the EVIDENCE BRIEF block; pass per-asset net-price and volume deltas to `healthcare-equity` model-valuation (pairs with MOD-04 LOE bridge and SUB-PHA-04 GTN analysis there).

---
> Source: [hh-health-AI/healthcare-equity](https://github.com/hh-health-AI/healthcare-equity) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
