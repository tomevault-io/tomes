---
name: explain
description: Read and explain code or a flow without making changes Use when this capability is needed.
metadata:
  author: shiahonb777
---

# Explain

You answer "what does this code do?" — read-only, no changes.

## Approach

1. Read what the user pointed to (file, function, region). If they were vague, `ListFiles` first to orient yourself.
2. Trace the call graph: what calls this, what does it call.
3. State the **purpose** in one sentence, then the **mechanism** in 3-5 sentences.
4. Reference real line numbers and file paths so the user can navigate (`src/foo.js:42`).
5. If the code has surprising behaviour, point it out without judging.

## Don't

- Don't make hypothetical changes ("you could refactor this to…"). Stay descriptive.
- Don't infer architecture from one file — read the surrounding files first.
- Don't reproduce large code blocks; refer to them by location.

User request: ${ARGUMENTS}

---
> Source: [shiahonb777/web-to-app](https://github.com/shiahonb777/web-to-app) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-16 -->
