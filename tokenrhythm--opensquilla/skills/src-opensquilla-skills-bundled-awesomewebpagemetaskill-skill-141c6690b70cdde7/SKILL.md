---
name: awesomewebpagemetaskill
description: Build a local multimedia webpage project from a user topic, audience, language, style, and media preferences by framing requirements, researching, planning, acquiring media, generating files, packaging, validating, repairing, and delivering usage guidance. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# AwesomeWebpageMetaSkill

Build a local multimedia webpage project from a topic, audience, language,
style, and media preference request.

Pipeline:

1. Requirement Framing
2. Deep Research
3. Page Outline (section structure + media intents; no filenames)
4. Media Acquisition (search / AIGC; producers emit `*_READY:` lines)
5. Media Assets Collect (deterministic path + existence check)
6. Webpage Source Generation
7. Deterministic Webpage Write
8. Deterministic Media Bind + Validation
9. Local Validation
10. Publish Complete Webpage Bundle
11. Delivery Guide

The current code-owned media capability candidate is OpenRouter. Its volatile
credential, endpoint, and proxy are leased from ordinary Provider Settings only
after the explicit media-send approval gate; they never enter this plan or a
persisted run. Non-secret media model defaults, output directory, and media
strategy remain configuration-owned, and individual steps must not invent them.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
