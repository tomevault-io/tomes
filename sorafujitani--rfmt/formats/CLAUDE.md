# rfmt

> A Ruby code formatter powered by a Rust native extension.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/rfmt/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# rfmt - Ruby Formatter

## Project Overview
A Ruby code formatter powered by a Rust native extension.

## Development Commands
```bash
# Run tests
bundle exec rspec

# Run the formatter
bundle exec rfmt <file>

# Build the Rust extension
bundle exec rake compile
```

## Claude Code Settings

### Plan File Location
Plan files created in plan mode should be saved to:
- **Preferred**: `.claude/plans/` (under the project root)
- Use the project-local `.claude/plans/`, not the global `~/.claude/plans/`

### Language
- Respond in Japanese

---
> Source: [sorafujitani/rfmt](https://github.com/sorafujitani/rfmt) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-05-05 -->
