---
name: rosclaw
description: - robot_state available Use when this capability is needed.
metadata:
  author: ros-claw
---
# SKILL.md

## Skill ID

`{namespace}/{name}`

## Intent

{name}

## Preconditions

- robot_state available

## Effects

- task_completed == true

## Runtime Contract

- Input: robot_state
- Output: trace + runtime_events

## Safety Envelope

- sandbox_first

## Evidence

- See `evidence/reports/`

---
> Source: [ros-claw/rosclaw](https://github.com/ros-claw/rosclaw) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
