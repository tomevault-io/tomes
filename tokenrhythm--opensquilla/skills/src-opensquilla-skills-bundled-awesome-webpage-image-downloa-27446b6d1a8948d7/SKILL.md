---
name: awesome-webpage-image-download
description: Deterministic image downloader for AwesomeWebpageMetaSkill search results. Use as skill_exec to fetch candidate image URLs into the configured local project tree without sandboxed shell curl. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# AwesomeWebpage Image Download

Internal deterministic downloader used by `AwesomeWebpageMetaSkill` after the
bounded web-search step has produced candidate image URLs.

It receives normalized media slots and search output on stdin, downloads direct
image URLs with Python HTTP APIs, validates the response MIME/magic bytes, saves
files by `slot_id`, and emits `IMAGE_READY:` records plus
`IMAGE_DOWNLOAD_INCOMPLETE:` when any requested image slot remains unfilled.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
