---
name: meta-skill-creator
description: Create or propose a new meta-skill that explicitly orchestrates multiple existing Skills, with trigger-collision, lint, smoke, and preview gates. Do not use for a standalone Skill, conceptual questions, pasted catalogs, or discussion of existing MetaSkills. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# Meta-Skill Creator

Safeguarded DAG that synthesizes a new bundled meta-skill from observed skill
co-occurrence patterns + user description of the desired workflow. It now
separates preview-only, persisted-proposal, and fully gated modes so lightweight
requests do not pay for persistence or smoke testing. The workflow separates
generic skill creation from meta-skill composition, checks trigger collisions,
classifies operational risk, and previews the proposal before optional
persistence.

Output is a SKILL.md candidate written to `~/.opensquilla/proposals/<id>/`.
By default it is not auto-loaded; run `opensquilla meta accept <id>` (Phase 2)
to enable. If the operator has enabled the auto-propose `auto_enable` setting,
this manual path also runs the same conservative static safety preflight used by
cron/dream auto-propose and may promote a low-risk gated proposal immediately.

## Fallback

If creator's pipeline fails at any step, **report the failure verbatim** to the
user:

1. State which step failed (e.g. "harvest", "lint")
2. Quote the error message from the orchestrator's structured log
3. Stop. Do NOT improvise.

Do NOT:
- Claim a proposal was written unless you have verified it by reading
  `~/.opensquilla/proposals/<id>/SKILL.md` with the `read_file` tool
- Invent file paths, proposal IDs, or skill names that you have not seen
  in the orchestrator's actual output
- "Manually run" the individual skills as a recovery — that bypasses
  the validation gates the user explicitly opted into

If the user wants to retry, suggest they re-issue the request after the
underlying error is resolved (often a sandbox or provider issue), not a
manual workaround.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
