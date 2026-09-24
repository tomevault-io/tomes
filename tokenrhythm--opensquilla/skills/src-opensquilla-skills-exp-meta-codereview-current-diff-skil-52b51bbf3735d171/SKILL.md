---
name: meta-codereview-current-diff
description: Read the current uncommitted diff, run three independent reviewers (safety + tests-coverage + style) in parallel, then arbitrate a single BLOCK / BLOCK_WITH_OVERRIDE / PASS_WITH_NOTES verdict. Use before commit when you want a multi-perspective second-opinion instead of a single-reviewer agent loop. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# Codereview of Current Diff (Meta-Skill)

A **combinator-style** meta-skill that runs three independent
reviewers in parallel over the currently-uncommitted diff, then
arbitrates a single verdict with a strict priority rule.

This is the same combinator + arbitrate pattern as
`meta-security-review-bundle`, applied to a code-review domain. The
three reviewers each carry a tight, project-specific rubric — safety
focuses on injection / credentials / G1.6 contract; tests focuses on
the "new public surface ⇒ corresponding test" expectation; style
flags only a fixed list of antipatterns so it doesn't drift into
free-form opinions.

## Trigger surface

Fire by saying `multi-reviewer diff`, `codereview my diff`, or one of the
localized triggers listed in the frontmatter. The diff is read from the working
tree (`git diff --cached HEAD`, falling back to `git diff HEAD` if nothing is
staged).

## Fallback

If `read_diff` returns `NO_DIFF`, the downstream reviewers should
reply with their respective clean verdicts ("CLEAR" / "PASS" /
"CLEAN") and arbitrate emits `PASS_WITH_NOTES: clean`. If a reviewer
LLM step fails, the orchestrator's partial outputs are visible in
`step_outputs`; operator should manually re-run the failed reviewer.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
