---
name: meta-diagram-triangulation
description: Scan a target codebase path, classify the most informative diagram kind, then render it as BOTH a PlantUML source file AND a draw.io XML in parallel, and compose them into a single architecture doc. Use when writing an RFC or onboarding doc and you want a text-friendly (PlantUML) and an editable (drawio) view of the same architecture. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# Diagram Triangulation (Meta-Skill)

A **classifier + parallel render** meta-skill. After scanning a target
path, an `llm_classify` step picks the most informative diagram kind
(one of `class | sequence | component | deploy | flow`), then **two
independent render branches** synthesize PlantUML source and draw.io
XML for the same scan — running in parallel because they are
independent tools serving different downstream uses (git-friendly text
review vs. editable canvas).

## Trigger surface

Fire by saying `diagram triangulation` or one of the localized triggers listed
in the frontmatter, with the target path or module reference in the same turn.

## Fallback

If either render step fails, `compose_doc` should still produce the
docx referencing whichever render succeeded; manually re-run the
failed render via `sub-agent` with the same scan output as input.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
