---
name: issue-spec-verify
description: Run final issue-spec verification across traceability, questions, review findings, PR rationale, PR checks, and durable spec draft. Use when this capability is needed.
metadata:
  author: higress-group
---

# Issue Spec Verify

Use when the user asks for /issue-spec:verify, issue-spec verify, or final readiness evidence before merge/archive.

## Steps

1. Run focused project tests and record evidence in VERIFY comments.
2. Run issue-spec verify-links --repo higress-group/higress --proposal <issue> --design <issue> --implement <issue> --json.
3. Render a durable spec draft:

       issue-spec archive durable-spec --repo higress-group/higress --proposal <issue> --capability <capability> --output /tmp/<capability>-spec.md --json

4. Run final verify:

       issue-spec verify --repo higress-group/higress --proposal <issue> --design <issue> --implement <issue> --pr <pr> --durable-spec /tmp/<capability>-spec.md --json

5. Final verify must fail if blocking questions, missing links, missing PROCESS rationale, open P0/P1 findings, failed or pending PR checks, or durable spec omissions exist.

---
> Source: [higress-group/higress](https://github.com/higress-group/higress) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
