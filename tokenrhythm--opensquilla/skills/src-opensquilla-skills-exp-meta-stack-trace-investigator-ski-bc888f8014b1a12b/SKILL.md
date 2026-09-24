---
name: meta-stack-trace-investigator
description: Use this meta-skill instead of answering directly when the user gives a stack trace, traceback, runtime error, or failing log that benefits from multi-skill orchestration across trace parsing, repo/history inspection, patch-target analysis, reproduction guidance, and verification commands.
metadata:
  author: TokenRhythm
---

# Stack-Trace Investigator (Meta-Skill)

A **combinator-style** meta-skill that converts a pasted stack trace into a
structured root-cause report. It now classifies Python, JavaScript,
TypeScript, Go, Rust, or unknown traces before running the investigation. After
parsing the trace once, heterogeneous investigations run in parallel:

1. **`grep_repo`** — ripgrep for the symbols in the current repo
2. **`search_issues`** — `gh issue list` for similar reported problems
3. **`git_history`** — recent commits touching the affected files
4. **`diff_context`** — `git-diff` skill for current worktree context
5. **`history_patterns`** — `history-explorer` skill for prior skill/router
   usage patterns
6. **`memory_recall`** — prior incidents stored under the `traceback` topic
7. **`language_probe`** — routed to the language-specific helper skill
   (`stack-trace-python-probe`, `stack-trace-js-probe`,
   `stack-trace-go-probe`, `stack-trace-rust-probe`, or generic fallback)

The `root_cause` and `repro_suggestion` steps fan the signals into a
hypothesis, concrete fix targets, and verification commands. The final summary
labels degraded evidence sources explicitly before persisting the incident.

## Trigger surface

Fire by saying `investigate stack trace` or one of the localized triggers
listed in the frontmatter, with the traceback pasted into the same turn.

## Fallback

If any leaf step fails, the orchestrator surfaces partial outputs in
`step_outputs`. Operator should manually run `rg <symbols>`,
`gh issue list --search`, `git log`, and `memory search` and
synthesize the report by hand.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
