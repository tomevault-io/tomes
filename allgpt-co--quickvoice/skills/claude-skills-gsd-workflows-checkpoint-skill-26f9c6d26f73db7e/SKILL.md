---
name: gsdworkflowcheckpoint
description: Workflow for managing checkpoints Use when this capability is needed.
metadata:
  author: allgpt-co
---

# GSD Checkpoint Workflow

Workflow for creating and managing checkpoints.

## When to Use

- Between waves
- Phase boundaries
- User interaction points

## Phases

1. Create checkpoint
2. Document progress
3. Request approval
4. Continue or complete

## Entry Points

- `gsd:create-checkpoint` - Create new checkpoint
- `gsd:update-checkpoint` - Update checkpoint
- `gsd:complete-checkpoint` - Complete checkpoint
- `gsd:continue-phase` - Continue from checkpoint

## Success Criteria

Checkpoint approved and phase continues.

---
> Source: [allgpt-co/QuickVoice](https://github.com/allgpt-co/QuickVoice) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-19 -->
