---
name: ktor
description: > Use when this capability is needed.
metadata:
  author: nomisRev
---

# Ktor Service Skill

Apply these conventions when implementing or reviewing Ktor code in this repository. Load only the references needed for the current task.

## Service architecture and wiring

Read [references/service-architecture.md](references/service-architecture.md) when changing application bootstrap (`Main.kt`/`SuspendApp`), `Env` configuration loaded from `application.yaml`, `Dependencies` wiring, or `ResourceScope`-based resource lifecycle.

## Package structure

Read [references/package-structure.md](references/package-structure.md) when creating, moving, or reorganizing files within a service module. Follow domain-driven feature packages, not technical layers.

## Routes and validation

Read [references/routes-and-validation.md](references/routes-and-validation.md) when editing HTTP contracts (Spine `Api.kt` endpoints), route handlers, `DomainError` modelling/mapping, or `accumulate`-based validation.

---
> Source: [nomisRev/ktor-arrow-example](https://github.com/nomisRev/ktor-arrow-example) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-07 -->
