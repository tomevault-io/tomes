---
name: meta-arxiv-daily-digest-deck
description: Fetch the day's top arXiv submissions in a chosen category, write a structured per-paper digest, render the digest as a PPTX deck (one slide per paper), and persist the digest to long-term memory. Use for a daily 'arxiv morning briefing' — manual fire or cron-scheduled. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# arXiv Daily Digest Deck (Meta-Skill)

A near-pure **`tool_call` + linear DAG** meta-skill: fetch arXiv via
the public Atom API, write a per-paper structured digest, render it
into a PPTX deck, and persist the digest into long-term memory under
the `arxiv-daily` topic.

## Trigger surface

Fire manually with the English trigger `arxiv daily digest` or one of the
localized triggers listed in the frontmatter. Category override: include a
`cs.XX` token anywhere in the invocation.

## Fallback

If `fetch_arxiv` fails (network or parse), the downstream steps
short-circuit by emitting `_SKIPPED` markers; no half-baked PPTX or
memory note is written. Operator can retry by re-invoking, or
manually run `curl 'http://export.arxiv.org/api/query?…'`.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
