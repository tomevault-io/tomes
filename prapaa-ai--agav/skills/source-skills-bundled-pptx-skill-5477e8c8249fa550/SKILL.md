---
name: pptx
description: Create and edit PowerPoint .pptx presentations Use when this capability is needed.
metadata:
  author: prapaa-ai
---

# PowerPoint Presentations (pptx)

Create and edit PowerPoint .pptx slide decks.

## Instructions

1. Check that the `python-pptx` library is available: run `python -c "import pptx"`. If it fails, install it with `pip install python-pptx` (requires user approval) and tell the user if installation is not possible.
2. If the user gave a topic but no outline, propose a slide outline first (title, agenda, content sections, summary) and get their approval before generating the deck.
3. For each slide, choose an appropriate layout: Title layout for the first slide, Title and Content for most others, Section Header to separate major parts. Use the deck's template placeholders rather than free-floating text boxes so the theme stays intact.
4. Keep slides scannable: a short title, at most 4-6 bullets per slide, and no full paragraphs. Put the detail in speaker notes (`slide.notes_slide.notes_text_frame`) instead.
5. Apply one consistent font size scheme across the deck (e.g. titles 32-40pt, body 18-24pt). Insert images only from files the user provided or pointed to.
6. When editing an existing deck, preserve its theme, masters, and untouched slides; modify only the slides requested.
7. Never overwrite the original file when producing a revised deck — write to a new file (e.g. `pitch-v2.pptx`) unless the user explicitly asks to modify in place.
8. After writing, verify by reopening the file and reporting: slide count, titles of each slide, and whether speaker notes were added.

---
> Source: [prapaa-ai/agav](https://github.com/prapaa-ai/agav) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-22 -->
