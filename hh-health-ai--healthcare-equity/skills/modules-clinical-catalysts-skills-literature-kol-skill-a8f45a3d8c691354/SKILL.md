---
name: literature-kol
description: > Use when this capability is needed.
metadata:
  author: hh-health-AI
---

# Literature & KOL Scan

Turn the medical literature and conference flow into investment signal: abstract triage, evidence-momentum reads, and KOL mapping.

## Conference abstract triage

1. When titles drop ahead of a conference, run SUB-BIO-03 (in `${CLAUDE_PLUGIN_ROOT}/skills/literature-kol/references/prompts.md`): per covered name — what the abstract reports · prior data bar · stock-moving likelihood · session timing · competing assets to watch · top 3 for detailed read.
2. Respect embargo staging (`${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`): state exactly what is public now — title-level vs abstract text vs full presentation — and never present title-implied results as data.

## Evidence-momentum scan

1. Use the PubMed connector to sweep recent publications for the asset/mechanism/indication: pivotal results, real-world evidence, meta-analyses, guideline updates, and editorials. Time-window the search and report counts honestly (publication momentum ≠ clinical superiority).
2. Grade what you find by evidence hierarchy — RCT > large registry/RWE > single-arm > case series > opinion — and by journal/guideline weight. Extract the two or three findings that would move a model variable, and translate per references/evidence-translation-clinical.md.
3. For preprints, use the biorxiv connector (if installed) and label non-peer-reviewed status explicitly.

## KOL mapping

1. Identify the field's voices from authorship patterns (last/corresponding authors on pivotal and guideline papers) and trial leadership (Clinical Trials connector investigator data). Note guideline-committee membership and disclosed conflicts (trial sponsorship).
2. Output a ranked KOL shortlist with affiliation, why they matter, and the one question each could uniquely answer — feed it to provider-adoption kol-site-map (site overlap) and healthcare-equity meetings-experts (EN-01 call prep). Keep MNPI guardrails: public positions only.

End substantive analyses with the EVIDENCE BRIEF block (layer: clinical or competitive as applicable).

---
> Source: [hh-health-AI/healthcare-equity](https://github.com/hh-health-AI/healthcare-equity) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-10-05 -->
