# llm-agents-ecosystem-handbook

> A research agent that produces sourced briefings on a topic. Reads multiple web sources, deduplicates, and writes a structured Markdown report with citations.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/llm-agents-ecosystem-handbook/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# AGENTS.md — Research agent

## Project
A research agent that produces sourced briefings on a topic. Reads multiple web sources, deduplicates, and writes a structured Markdown report with citations.

## Conventions
- All claims in the final report must include a citation `[n]` linking to a real URL retrieved during the run
- Never fabricate sources. If a fact has no source, label it as `(unsourced)` and flag it
- Prefer 5–10 high-quality sources over 30 mediocre ones

## Workflow
1. Plan sub-questions
2. Search + fetch (use Skills/research-summarizer)
3. Cluster + dedupe findings
4. Draft report with citations
5. Self-review against the rubric in `evals/`

## Don'ts
- Don't include personal opinions
- Don't follow links from inside fetched pages without re-evaluating the source

---
> Source: [oxbshw/LLM-Agents-Ecosystem-Handbook](https://github.com/oxbshw/LLM-Agents-Ecosystem-Handbook) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-21 -->
