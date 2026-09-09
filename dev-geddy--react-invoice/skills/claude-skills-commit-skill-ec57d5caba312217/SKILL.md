---
name: commit
description: > Use when this capability is needed.
metadata:
  author: dev-geddy
---

# commit

Repo commit convention. One rule set, no exceptions.

## Format
- **Semantic one-liner only.** `type(scope): subject` — single line, nothing else.
- **No body.** No blank line + paragraphs. No bullet lists.
- **No trailers / footers.** No `Co-Authored-By`, no `Generated with`, no issue refs unless asked.
- Imperative mood, lowercase subject, no trailing period. Aim ≤72 chars.

## Types
`feat` `fix` `docs` `chore` `refactor` `style` `test` `build` `ci` `perf`

## Scope
Optional. Package/area: `web`, `ui`, `auth`, `docs`, … Use when it sharpens meaning.

## Examples
- `feat(auth): add google login callback`
- `fix(ui): mount tooltip provider in root layout`
- `chore(web): run dev server on port 3080`
- `docs: bootstrap three-level doc system`

## Do NOT
- Multi-line bodies, "why" paragraphs, checklists.
- `Co-Authored-By:` or any co-author trailer.
- Tool/agent attribution footers.

## Commit command
`git commit -m "type(scope): subject"` — single `-m`, one line.

---
> Source: [dev-geddy/react-invoice](https://github.com/dev-geddy/react-invoice) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-07 -->
