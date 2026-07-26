# krayon

> Krayon project architecture — module structure and conventions

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/krayon/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:


# Project Architecture

Krayon is a **Kotlin Multiplatform** monorepo of focused drawing/charting libraries published under `com.juul.krayon`.
Krayon draws heavy inspiration from [D3](https://github.com/d3/d3), reflecting its API when possible.

## Module Structure

- The full module list is in `settings.gradle.kts`. Each module's dependencies are in its own `build.gradle.kts`.
- Published KMP targets are defined in `build-logic/src/main/kotlin/library-conventions.gradle.kts`.
- `core` is the foundational module with no internal dependencies.
- `box` is a convenience aggregate that re-exports all published libraries — avoid adding new code there.
- `compose` is the Compose Multiplatform bridge.
- `sample` is the demo app (not published).

## Key Conventions

- Each published library applies `library-conventions` from `build-logic/`.
- Package names follow `com.juul.krayon.<module>` (hyphens become dots for Android namespace).

---
> Source: [JuulLabs/krayon](https://github.com/JuulLabs/krayon) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-07-26 -->
