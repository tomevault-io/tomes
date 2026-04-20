# whisper-money

> - Make sure that CI steps are passing (`.github/workflows/ci.yml`).

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/whisper-money/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# After each change
- Make sure that CI steps are passing (`.github/workflows/ci.yml`).
  - bun install --frozen-lockfile
  - composer install --no-interaction --prefer-dist --optimize-autoloader
  - bun run build
  - ./vendor/bin/pest
  - vendor/bin/pint --test
  - bun run format
  - bun run lint

---
> Source: [whisper-money/whisper-money](https://github.com/whisper-money/whisper-money) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-04-20 -->
