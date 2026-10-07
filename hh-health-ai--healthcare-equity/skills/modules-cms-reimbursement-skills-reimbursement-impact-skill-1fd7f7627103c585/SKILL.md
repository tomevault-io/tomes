---
name: reimbursement-impact
description: > Use when this capability is needed.
metadata:
  author: hh-health-AI
---

# Reimbursement & Coding Change Impact

Turn a CMS rule or coverage/payment change into a per-procedure dollar delta and a name-level revenue and thesis impact.

## Workflow

1. Identify the event precisely: which rule (IPPS, OPPS/ASC, PFS, CLFS, NCD/LCD change, NTAP/TPT decision), proposed vs final, effective date, and the affected codes/APCs/DRGs. Pull rule specifics from cms.gov via web research; use the CMS Coverage connector for the coverage side.
2. Run the analysis using the SUB-MED-02 prompt in `${CLAUDE_PLUGIN_ROOT}/skills/reimbursement-impact/references/prompts.md` as the working template: rule details → dollar impact per procedure → volume impact → competitive impact → implementation timeline → thesis delta → engagement plan.
3. Quantify both price and behavior: a rate cut changes per-unit economics *and* site-of-service and adoption incentives (e.g., HOPD→ASC migration). Model each separately.
4. Separate proposed from final: proposed rules are a probability-weighted catalyst (note the comment-period end and final-rule date); final rules are a model update.
5. Cross-check who actually bears the change — provider economics vs device ASP vs payor MLR — before assigning the impact to a ticker. The company whose procedure is repriced is not always the company whose P&L moves.
6. End with the EVIDENCE BRIEF block, and hand the model-variable changes to `healthcare-equity` model-valuation (and the event dates to the catalyst calendar).

## Data discipline

State the rule year and version (proposed/final/corrected) on every number. Payment rates come from the fee-schedule files, coverage from the MCD — cite both when both move.

---
> Source: [hh-health-AI/healthcare-equity](https://github.com/hh-health-AI/healthcare-equity) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
