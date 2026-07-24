---
name: counterfact
description: > Use when this capability is needed.
metadata:
  author: counterfact
---

# Counterfact Skill

## Purpose

Give agents a quick, practical overview of Counterfact so they can safely edit
Counterfact-generated projects.

## What Counterfact is

Counterfact generates a working mock API from an OpenAPI/Swagger specification.
It creates route handler files and types, then runs a live server with hot
reload and a REPL.

## How Counterfact works

1. Parse an OpenAPI spec.
2. Generate route handlers under `routes/` and types under `types/`.
3. Serve endpoints through the generated handlers.
4. Keep mutable runtime state in `_.context.ts` files.
5. Seed/modify state via `scenarios/` and REPL scenario commands.

## Editing guidance

- Treat `routes/` as the place for HTTP glue (status code + response mapping).
- Put business logic/state mutation in context classes, not handlers.
- Use scenarios for dummy data and reusable setup flows.

## Documentation

- https://counterfact.dev

---
> Source: [counterfact/api-simulator](https://github.com/counterfact/api-simulator) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-14 -->
