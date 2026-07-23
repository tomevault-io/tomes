---
name: e2e-coverage-check
description: > Use when this capability is needed.
metadata:
  author: incubateur-ademe
---

# E2E Coverage Check

Analyze whether current branch changes require new or updated e2e tests.

## When to Use

- After completing a feature implementation, before creating a PR
- When changes touch views, wizard steps, routes, controllers, or shared DTOs
- To verify that new user-facing flows have adequate e2e test coverage

## Instructions

1. Launch the `e2e-coverage-checker` agent with this prompt:

   > Analyze the current branch's changes against main and produce an e2e coverage check report. Follow your instructions step by step: collect the diff, classify files, run the deep pass where needed, map coverage, and generate the report.

2. Relay the agent's report to the user exactly as produced. Do not summarize or modify it.

---
> Source: [incubateur-ademe/benefriches](https://github.com/incubateur-ademe/benefriches) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-14 -->
