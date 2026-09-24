---
name: meta-migration-assistant
description: Use this meta-skill instead of answering directly when the user needs a concrete migration plan that benefits from multi-skill orchestration across migration classification, authoritative guide lookup, optional repo diff inspection, and step-by-step validation planning.
metadata:
  author: TokenRhythm
---

# Migration Assistant (Meta-Skill)

Take a "help me migrate X → Y" request and produce a concrete, runnable
checklist. The pipeline does four things:

1. **classify** the migration kind via an LLM tag (one of six tokens).
2. **fetch_guide** the most authoritative source for THAT migration:

   | Classifier verdict          | Best source            | Routed skill          |
   |-----------------------------|------------------------|-----------------------|
   | `OPENAI_V0_TO_V1`           | repo release notes     | `github`              |
   | `PY2_TO_PY3`                | framework migration doc| `multi-search-engine` |
   | `VUE2_TO_VUE3`              | framework migration doc| `multi-search-engine` |
   | `REACT_CLASS_TO_HOOKS`      | framework migration doc| `multi-search-engine` |
   | `CJS_TO_ESM`                | (fuzzy, synthesize)    | `multi-search-engine` |
   | `OTHER` (default)           | (synthesize)           | `deep-research`       |

3. **repo_context** optionally inspects the current repo diff only when the
   prompt indicates that local repository context should shape the migration.

4. **write_plan** uses a constrained `llm_chat` renderer so explicit source
   and target terms in the user request remain authoritative even when
   repository context or retrieved guide text is noisy.

## Fallback

If the orchestration fails: ask the user to specify the migration tag
manually, run the matching skill yourself, then write the checklist.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
