---
name: project-stats
description: >- Use when this capability is needed.
metadata:
  author: EchoYue-lp
---

## Project Statistics

Skill directory: ${SKILL_DIR}
Session: ${SESSION_ID}

You have access to scripts that analyze codebases. Use them to answer questions
about project size, composition, and health.

### Environment Info

Current host: !`uname -s 2>/dev/null || echo unknown`

### Available Scripts

| Script | Purpose | Usage |
|--------|---------|-------|
| `scripts/count_lines.py` | Count lines of code by language | `run_skill_script("project-stats", "scripts/count_lines.py", "<directory>")` |
| `scripts/find_todos.sh` | Find TODO/FIXME/HACK comments | `run_skill_script("project-stats", "scripts/find_todos.sh", "<directory>")` |
| `scripts/dep_summary.ts` | Summarize project dependencies | `run_skill_script("project-stats", "scripts/dep_summary.ts", "<directory>")` |

### Workflow

1. Ask the user for the project path (or use the current directory)
2. Run `count_lines.py` to get an overview of languages and code volume
3. Run `find_todos.sh` to surface technical debt markers
4. If the project has `package.json` or `Cargo.toml`, run `dep_summary.ts` for dependency info
5. Synthesize findings into a concise report

### Output Format

Present results as a structured report with sections:
- **Overview**: total files, total lines, primary language
- **Language Breakdown**: table of language → files → lines → percentage
- **Technical Debt**: TODO/FIXME count and notable items
- **Dependencies** (if applicable): direct vs dev dependency count

---
> Source: [EchoYue-lp/echo-agent](https://github.com/EchoYue-lp/echo-agent) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
