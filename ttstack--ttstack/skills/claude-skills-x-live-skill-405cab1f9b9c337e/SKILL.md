---
name: x-live
description: Plan and run bounded TTstack lifecycle, guest, networking, and restart checks on an authorized Linux host. Use only when the user explicitly invokes /x-live. Use when this capability is needed.
metadata:
  author: TTstack
---

# Lightweight TTstack Live Validation

Functional acceptance on a real host. Not benchmarking, not production deployment,
not a security certification.

## Input

`$ARGUMENTS` — the behavior, defect, or environment to validate. Empty → the
uncommitted task change; with no change either, ask instead of guessing a scope.

## Setup

Read `.claude/docs/host-validation.md`, `docs/guest-images.md`, and the most relevant
dated report for useful cases and the limits of earlier evidence. Prior reports are not
permission to reuse a host or repeat every test.

## Protocol

1. **Bound the experiment** (`host-validation.md`): authorization, host prerequisites,
   the half-host budget, isolation, and the list of created resources.
2. **Verify the relevant behavior**: select cases from the actual change rather than
   running the whole list. Distinguish normal shutdown from forced termination, and
   guest or application readiness from a live VMM process.
3. **Close the loop**: clean up task-owned resources, confirm pre-existing services
   still hold their expected state, and write a dated report when evidence is retained.
4. A reproducible defect feeds a focused change; rerun only the affected checks.

## Output

Host and tested revision · cases observed and omitted · results including which
shutdown kind was seen · cleanup state · limits and untested scope · keys and private
configuration excluded.

---
> Source: [TTstack/TTstack](https://github.com/TTstack/TTstack) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-29 -->
