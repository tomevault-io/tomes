# hydro

> Use [Conventional Commits](https://www.conventionalcommits.org/) format:

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/hydro/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Agent Guidelines

## Commit Messages

Use [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>[optional scope]: <short summary>

<markdown body>
```

Types: `feat`, `fix`, `refactor`, `docs`, `test`, `chore`, `ci`, `perf`.

For breaking changes, append `!` after the type (e.g. `refactor(hydro_lang)!:`), and add `BREAKING CHANGE: ...` footers
describing each breaking change (or summarizing if many).

## Descriptions

Write the description in **Markdown**. Use bullet lists, code spans, and headings to organize multi-topic changes. Example:

```
feat(hydro_lang): ...

... detailed explanation of key design decisions
```

---
> Source: [hydro-project/hydro](https://github.com/hydro-project/hydro) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-08-09 -->
