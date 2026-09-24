---
name: meta-scheduled-morning-digest
description: Compose a morning digest combining local weather, news for the user's interest topic, a structured summary, and a memory note. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# Scheduled Morning Digest (Meta-Skill)

Pulls today's weather and news on a topic, summarizes them, and records
the digest in long-term memory for later recall. The MVP runs once per
invocation; recurring scheduling is left to the host (`cron` skill or
external scheduler) and is intentionally out of scope here.

## Fallback

Have the LLM call `weather`, then `multi-search-engine`, summarize, and
finally `memory_save` manually.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
