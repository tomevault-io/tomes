---
name: overview
description: Diagram existing product, journey, and architecture overlays. Use when the user types /overview. Use when this capability is needed.
metadata:
  author: blockmatic
---

## Purpose and inputs

Render an overview from existing FIRST overlays and technical docs. Do not let the codebase become the product brief. Chat only unless the user names a file.

## Steps

1. Load FIRST in the repository's order. Read `PRODUCT.md`, `JOURNEYS.md`, and `ARCHITECTURE.md` (or the instance paths in `FIRST.md`).
2. If an overlay is missing, stop for that view and point at `/f-product`, `/f-journeys`, or `/f-architecture`.
3. Draw at most two Mermaid diagrams that restate those overlays. Use code only to label what already exists.
4. Output in chat: a short factual summary plus the diagrams. No invented narrative.

## Verification

- [ ] Diagram nodes map to overlay facts or documented components.
- [ ] Missing overlays were reported, not filled from a scan.
- [ ] No files were written unless requested.

## Handoff

Cite the overlay paths used. Durable changes go through `/f-*`, not this playbook.

---
> Source: [blockmatic/basilic](https://github.com/blockmatic/basilic) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-08 -->
