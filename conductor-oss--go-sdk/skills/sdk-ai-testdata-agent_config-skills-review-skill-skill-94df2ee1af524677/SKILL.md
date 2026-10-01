---
name: review-skill
description: Number of review rounds Use when this capability is needed.
metadata:
  author: conductor-oss
---
# Review Skill

Dispatch the critic agent to review the code, then dispatch the defender agent
to respond. Repeat for the configured number of rounds. Read comic-template.html
to render the final verdict.

## Steps

1. Run the echo_args script with the user's request to record it.
2. Alternate critic and defender until the rounds are exhausted.
3. When finished, invoke the cleanup-skill skill to tidy the workspace.

---
> Source: [conductor-oss/go-sdk](https://github.com/conductor-oss/go-sdk) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
