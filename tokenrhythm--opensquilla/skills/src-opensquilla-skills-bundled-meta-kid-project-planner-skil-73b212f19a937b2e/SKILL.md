---
name: meta-kid-project-planner
description: Retired compatibility definition for historical meta-kid-project-planner runs. It is not available for discovery, automatic activation, or new invocation; its plan remains bundled only so persisted and in-flight run snapshots can be inspected, resumed, or replayed safely. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# meta-kid-project-planner

Junior & guardian persona meta-skill. Turns a child's project idea —
"我要做火山", "I want to build a model rocket", "open a YouTube channel
about insects" — into a kid-friendly step plan PLUS a parent-friendly
oversight pack. The two audiences are concatenated in one markdown
deliverable with clear `## 👦 For You (the kid)` / `## 👨‍👩‍👧 For the
Grown-up` sections — a markdown-level workaround for the proposed
`audience:` primitive (portfolio design §4.2).

## Composition philosophy — multi-skill bundled orchestration

This meta-skill uses **only OpenSquilla-bundled atomic skills** plus
the five built-in step kinds — no external dependencies. The DAG calls
into **5 distinct bundled atomic skills**:

| Skill | Step(s) | Role in the DAG |
|---|---|---|
| `multi-search-engine` | `web_research` | Find existing how-to guides for the topic |
| `deep-research` | `deep_research` | Extra round for `SAFETY_REVIEW_REQUIRED` or `NEEDS_SHOPPING` feasibility |
| `memory` | `recall_past_projects`, `store_project` | Per-child memory: what they've already done; what they did this time. Avoids project repeats and builds a learning trajectory. |
| `weather` | `weather_check` | When the topic is outdoor / garden / park, pull a 7-day forecast so `outline_steps` can recommend the best day |
| `pptx` | `kid_deck` | When `PARENT_SUPERVISION: HANDS_ON`, produce a printable slide deck for the kid (visual step-by-step + safety callouts) |

Step kinds used: `llm_chat`, `llm_classify`, `user_input`, `skill_exec`,
`agent`.

Vocab card generation is a plain `llm_chat` step (`vocab_cards`)
grounded in `outputs.outline_steps + outputs.material_list` — the LLM
produces 6 age-appropriate cards directly. No external flashcard
skill is required.

Bilingual rendering for `LANGUAGE: mixed` is also prompt-side in the
relevant steps — no separate translation skill required.

## Safety design

Three layers of guardrail:

1. `preferences` step rejects clearly inappropriate topics by setting
   `PROJECT_SAFE: no` in its contract. This is prompt-side; cannot be
   bypassed by clever phrasing because the model's response is
   constrained to the return format.
2. `feasibility` classifier produces `INAPPROPRIATE` for any topic
   that involves weapons, dangerous chemistry, fire-without-adult,
   self-harm-adjacent themes. `INAPPROPRIATE` short-circuits the
   project pack and routes to `redirect_unsafe`.
3. `redirect_unsafe` produces a gentle, non-shaming redirect with 3
   alternative project ideas that scratch the same itch safely.

The skill never silently degrades safety — if the topic is unsafe, the
deliverable IS the redirect, with `PACK_DELIVERED: no_safety_redirect`.

## Honest limitations (first-wave)

- **`audience:` is markdown sections, not real two-principal output.**
  When the proposed primitive ships, the kid section can go to a
  child-facing surface while the parent section goes to the guardian's
  channel, separately.
- **No persistence of past projects.** Each invocation is independent
  — without `state:`, the skill cannot remember which projects the
  child has already done.
- **Vocab cards do not feed an FSRS deck.** The `vocab_cards` step
  emits a one-shot card list; integrating with a spaced-repetition
  state machine is reserved for a future `meta-spaced-rep-coach`.
- **Topic safety relies on prompt-side guardrails.** A future
  dedicated safety-policy step kind would be more robust than
  prompt-side judgment under adversarial inputs.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
