---
name: docs-knowledge-base
description: > Use when this capability is needed.
metadata:
  author: agglayer
---

Use this workflow when creating or editing files under `docs/knowledge-base/`.

## Audience and tone

- Primary audience: human maintainers and contributors.
- Secondary audience: AI agents reading project documentation.
- Write concise, factual prose.
- Avoid AI-specific annotations or prompt-oriented formatting.

## mdbook structure

- Keep chapter sources under `docs/knowledge-base/src/`.
- Keep `docs/knowledge-base/src/SUMMARY.md` as the navigation source of truth.
- When adding a new chapter,
  update `SUMMARY.md` in the same change.

## Chapter format

- One top-level heading (`#`) per chapter.
- Prefer short sections with explicit responsibilities,
  invariants,
  and workflows.
- Link related terms to `glossary.md`.
- Link to relevant code paths when making concrete claims.

## Writing conventions

- Follow semantic line breaks for prose.
- Prefer active voice and operational wording.
- Keep guidance implementation-neutral unless a path is repository-specific.
- Clearly separate facts,
  constraints,
  and recommendations.

## Verification

Before finishing,
build the book and report the exact command and result:

```bash
mdbook build docs/knowledge-base/
```

---
> Source: [agglayer/agglayer](https://github.com/agglayer/agglayer) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
