# renux

> Notes for agents working on renux (TUI bulk file renamer).

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/renux/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# AGENTS.md

Notes for agents working on renux (TUI bulk file renamer).

## Layout

- `src/renux/tags.py` - placeholder/filter registry (see above)
- `src/renux/parser.py` - resolves tag strings against filenames
- `src/renux/renamer.py` - actual rename/apply logic
- `src/renux/backup.py` - undo/backup support for applied renames
- `src/renux/app.py`, `screens/`, `components/` - Textual TUI
- `src/renux/cli.py` - CLI entrypoint (`renux` console script)

## Testing

`poetry run pytest` and `poetry run mypy src` before considering a change done.
Both are also enforced in CI/preqcommit.

## Tags registry is the source of truth

`src/renux/tags.py` is a single registry for every `{placeholder}` and `{value|filter}`.
Adding/changing a placeholder or filter there is enough.
Docs, autocomplete, and README all derive from it via `src/renux/tags_reference.py`.
Don't hand-edit the tag docs elsewhere.

---
> Source: [andrianllmm/renux](https://github.com/andrianllmm/renux) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-09-24 -->
