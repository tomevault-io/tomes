---
name: meta-knowledge-base-bootstrap
description: Bootstrap a domain knowledge base from a single seed (URL / PDF path / git repo / free-text topic): classify source → ingest with the right tool → persist to memory + xlsx index. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# Knowledge Base Bootstrap (Meta-Skill)

Seed a domain knowledge base in one turn. The pipeline classifies the seed
source type (URL / PDF / GIT / TEXT) and ingests it via the
`multi-search-engine` skill, then persists the report and produces an
index.

| step       | kind          | skill                  | what it does                                |
|------------|---------------|------------------------|---------------------------------------------|
| classify   | `llm_classify`| —                      | label the seed as one of `URL / PDF / GIT / TEXT` |
| ingest     | `skill_exec`  | `multi-search-engine`  | run a DuckDuckGo search (JSON to stdout)    |
| memorize   | `tool_call`   | — (`memory_save`)      | append the ingestion summary to memory      |
| index      | `agent`       | `xlsx`                 | write `kb-index.xlsx` with the result table |

> The classifier is currently informational only — the ingest step always
> calls `multi-search-engine`. A previous design routed `PDF → pdf-toolkit`
> and `GIT → github`, but those branches were dropped when the DSL moved to
> `skill_exec`. A follow-up will reintroduce per-classification routing once
> the corresponding bundled skills also expose `entrypoint:` manifests.

## Fallback

If the meta-flow fails: run the classifier prompt manually, then invoke
the appropriate ingestion skill, then `memory_save` the result, then
create the xlsx index with openpyxl.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
