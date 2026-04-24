# clarc

> **clarc** is a production-grade Claude Code workflow OS — agents, skills, hooks, commands, rules, and a continuous learning flywheel for modern software engineering.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/clarc/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# clarc — Cursor Rules

**clarc** is a production-grade Claude Code workflow OS — agents, skills, hooks, commands, rules, and a continuous learning flywheel for modern software engineering.

## Architecture

- **agents/** — Specialized subagents (planner, code-reviewer, tdd-guide, etc.)
- **skills/** — Domain knowledge and patterns (`skills/<name>/SKILL.md`)
- **commands/** — Slash commands invoked by users
- **hooks/** — Trigger-based automations
- **rules/** — Always-follow guidelines (language-specific)
- **scripts/** — Cross-platform Node.js utilities

## Language-Specific Rules

Language rules are in `.cursor/rules/<lang>-*.md`. Active rules are selected by file extension automatically.

**Available language rule sets:**
- `typescript-*` — TypeScript/JavaScript (`.ts`, `.tsx`, `.js`, `.mjs`)
- `python-*` — Python (`.py`)
- `golang-*` — Go (`.go`)
- `java-*` — Java (`.java`)
- `swift-*` — Swift (`.swift`)
- `rust-*` — Rust (`.rs`)
- `cpp-*` — C++ (`.cpp`, `.cc`, `.h`, `.hpp`)
- `c-*` — C (`.c`)
- `csharp-*` — C# (`.cs`, `.razor`)
- `kotlin-*` — Kotlin (`.kt`, `.kts`)
- `scala-*` — Scala (`.scala`, `.sc`)
- `php-*` — PHP (`.php`)
- `ruby-*` — Ruby (`.rb`, `.rake`)
- `elixir-*` — Elixir (`.ex`, `.exs`)
- `r-*` — R (`.R`, `.Rmd`, `.qmd`)
- `bash-*` — Bash/Shell (`.sh`, `.bash`, `.zsh`)
- `sql-*` — SQL (`.sql`)
- `common-*` — Universal principles (all files)

## Global Coding Standards

### Immutability (CRITICAL)

Always create new objects, never mutate existing ones. Immutable data prevents hidden side effects and enables safe concurrency.

### Error Handling

Handle errors explicitly at every level. Never silently swallow errors. Use structured error types, not bare strings.

### Input Validation

Validate all user input at system boundaries. Fail fast with clear error messages.

### File Organization

Many small files over few large files. 200–400 lines typical, 800 max. Organize by feature/domain.

### Code Quality Checklist

- Code is readable and well-named
- Functions are small (<50 lines)
- Files are focused (<800 lines)
- No deep nesting (>4 levels)
- Proper error handling
- No hardcoded secrets or values
- No mutation (immutable patterns)

## Development Notes

- Package manager: npm, pnpm, yarn, or bun (auto-detected)
- Agent format: Markdown with YAML frontmatter (name, description, tools, model)
- Skill format: `SKILL.md` with frontmatter + When-to-Activate + examples
- Hook format: JSON with matcher conditions and command/notification arrays
- File naming: lowercase with hyphens (`python-reviewer.md`, `tdd-workflow.md`)

---
> Source: [marvinrichter/clarc](https://github.com/marvinrichter/clarc) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-04-24 -->
