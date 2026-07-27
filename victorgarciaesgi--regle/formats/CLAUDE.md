# regle

> On **every** Copilot code review, run these blocking checks before approving a pull request. See `.github/skills/code-review/SKILL.md` for full details.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/regle/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:


# Pre-commit validation (every code review)

On **every** Copilot code review, run these blocking checks before approving a pull request. See `.github/skills/code-review/SKILL.md` for full details.

## Required gates

1. **Commitlint** — validate every commit message (`printf '%s' "$MSG" | pnpm exec commitlint`). Format: `type(scope): subject` per `commitlint.config.ts`. Flag violations as blocking.
2. **pnpm workspace** — `test -f node_modules/.modules.yaml`; require `pnpm install` if missing.
3. **Lint** — `pnpm run lint` must exit 0.
4. **Format** — `pnpm run fmt:check` must exit 0.

Run from repo root after `pnpm install`.

Do not approve the PR until all gates pass or the author addresses every failure.

---
> Source: [victorgarciaesgi/regle](https://github.com/victorgarciaesgi/regle) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-27 -->
