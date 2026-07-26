# openagent

> Security, auth, and async tasks for LMForge API

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/openagent/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

Security & Async:
- Rate limiting: use existing Flask-Limiter patterns.
- Background tasks (>2s): ALWAYS use Celery with Redis broker (DB 1).
- Database: use SQLAlchemy sessions via Injector, always commit/rollback properly.
- Logging: use the project's structlog configuration.
- Validation: Pydantic for all inputs/outputs.

---
> Source: [Haohao-end/openagent](https://github.com/Haohao-end/openagent) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-26 -->
