---
name: community-research-insight
description: Extract structured insight briefs from community research transcripts or notes. Produces pain points, stakeholder needs, opportunity maps, risks, and follow-up questions. Requires human review before publication. Use when this capability is needed.
metadata:
  author: clawdotnet
---

# Community Research Insight Extractor

Extracts pain points, stakeholder needs, risks, and practical technology
opportunities from community-engaged research discussions. Produces a structured
insight brief for human review before publication.

## What It Does

| Step | Kind | Purpose |
| --- | --- | --- |
| `collect` | `user_input` | Collect transcript, context, and audience via chat |
| `analyze` | `llm_chat` | Extract grounded themes as structured JSON |
| `analyze_fallback` | `llm_chat` | Produce best-effort grounded JSON if primary analysis fails |
| `draft` | `llm_chat` | Draft the full 6-section insight brief as structured JSON |
| `validate` | `llm_chat` | Gate preview on PASS vs REVISE grounding validation |
| `validation_revise` | `llm_chat` | Explain why the brief is blocked when validation fails |
| `preview` | `llm_chat` | Render validated findings as human-readable Markdown |
| `review` | `user_input` | Pause for human approve/revise/reject decision |
| `final_response` | `llm_chat` | Produce final output based on review decision |

## Guardrails

- **Never** invent quotes, names, dates, or statistics.
- **Never** attribute views to named people unless present in the source.
- **Never** recommend replacing community engagement with automation.
- **Always** separate evidence from inference.
- **Always** flag missing information rather than filling gaps.
- **Always** require human review before publication or named attribution.

## Fallback

If `analyze` fails (timeout, provider error, or JSON contract failure),
`analyze_fallback` runs a single-turn `llm_chat` on the same transcript and must
satisfy the same JSON output contract. If `validate` returns REVISE, the preview
path is blocked and `validation_revise` explains what must be fixed before human
review.

## Output Contract

The `analyze`, `analyze_fallback`, and `draft` steps enforce `OutputContract` JSON
validation. The `draft` step requires `executive_summary`, `key_pain_points`,
`stakeholder_needs`, `opportunity_map`, `risks_and_cautions`, and
`follow_up_questions`.

## Safety

Outputs are decision-support drafts for human review. They are **not** final
professional advice in research, policy, or community engagement contexts.
Named attribution and external publication require explicit reviewer approval.

---
> Source: [clawdotnet/openclaw.net](https://github.com/clawdotnet/openclaw.net) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-24 -->
