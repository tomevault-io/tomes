---
name: zuoge
description: Refinement stage: **do not add graphics**. Unify, precise, subtract. Use when this capability is needed.
metadata:
  author: recombyn
---
# Polish / Subtraction (qa)

Refinement stage: **do not add graphics**. Unify, precise, subtract.

## Hard rules

Answer before any polish ops:

1. What can be deleted without losing information?
2. What can be merged (same function)?
3. What is duplicate?
4. What decoration does not strengthen the thesis?
5. Are there >1 primary focals? Keep one.

## Allowed actions

```text
remove · merge · simplify · align · reduce
```

## Forbidden during polish

```text
add · add · add
new particles · new glass cards · new icon rows
```

## Output for Review / Repair

Populate `subtraction_actions` with concrete removals/merges (living SCENE ids).
When score is 70–89, Host compiles a Repair Plan.
When score is 90+ (or about to settle), Host compiles one polish pass:
`remove · merge · simplify · align · reduce` — never `create_*`.

Hero, primary title, and full-bleed plates are protected.

## Checklist

- [ ] At least one subtraction considered
- [ ] No new decorative nodes
- [ ] Alignment / spacing tightened toward tokens

---
> Source: [recombyn/zuoge](https://github.com/recombyn/zuoge) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
