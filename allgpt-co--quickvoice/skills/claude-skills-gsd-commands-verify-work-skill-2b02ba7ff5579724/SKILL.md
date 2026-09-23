---
name: gsdverify-work
description: Verify completed work against requirements Use when this capability is needed.
metadata:
  author: allgpt-co
---

# GSD Verify Work

Verifies completed work using gsd-verifier agent to ensure requirements are met.

## When to Use

- After task completion
- Before checkpoint approval
- Validating implementation correctness

## Process

1. Load phase plan and task details
2. Run gsd-verifier agent
3. Check verification results
4. Report verification status

## Verification Checklist

- Code matches requirements
- Tests pass
- No regressions
- Documentation updated

## Success Criteria

All verification checks pass.

## Related Skills

@skills/gsd/agents/verifier - Agent that verifies implementation
@skills/gsd/commands/execute-phase - Executes phase tasks

---
> Source: [allgpt-co/QuickVoice](https://github.com/allgpt-co/QuickVoice) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-19 -->
