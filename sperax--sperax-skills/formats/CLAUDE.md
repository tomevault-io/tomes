# sperax-skills

> 38 open-source AI agent skills for DeFi, Web3, and the Sperax ecosystem.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/sperax-skills/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# GEMINI.md — Guidelines for Gemini

## Repository

38 open-source AI agent skills for DeFi, Web3, and the Sperax ecosystem.
Published to [ClawHub](https://clawhub.ai). Each skill = `skills/<slug>/SKILL.md`.

## Key Commands

- `./bin/validate.sh` — validate skills
- `./bin/publish-all.sh` — publish to ClawHub
- `./scripts/generate-llms-txt.sh` — regenerate LLM context

## Skill Format

YAML frontmatter (`name`, `description`, `metadata.openclaw`) + Markdown body.
Slugs: lowercase, hyphens, URL-safe. Min 100 lines. Tables + examples required.

## Content Policy

Read-only educational content only. No internal architecture, secrets, or executable code.
Gitmoji commit prefixes: `✨ feat:`, `📝 docs:`, `🐛 fix:`, `♻️ refactor:`.

---
> Source: [Sperax/sperax-skills](https://github.com/Sperax/sperax-skills) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-10-07 -->
