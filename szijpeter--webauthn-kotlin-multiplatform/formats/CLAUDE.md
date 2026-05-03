# webauthn-kotlin-multiplatform

> Canonical policy lives in `docs/ai/STEERING.md`.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/webauthn-kotlin-multiplatform/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Agent Adapter: Codex

Canonical policy lives in `docs/ai/STEERING.md`.

## Required Behavior

1. Apply `docs/ai/STEERING.md` as authoritative repository policy.
2. Prefer smallest viable change with targeted tests.
3. Run quality gates via `tools/agent/quality-gate.sh`.
4. When public API or publishing changes are involved, also run `apiCheck` and/or `publishToMavenLocal` as required by steering.
5. Keep token usage low: changed files first, no broad scans unless blocked.

## Standard Commands

Fast advisory:

```bash
tools/agent/quality-gate.sh --mode fast --scope changed --block false
```

Strict advisory before PR update:

```bash
tools/agent/quality-gate.sh --mode strict --scope changed --block false
```

API compatibility:

```bash
./gradlew apiCheck --stacktrace
```

Publishing preflight:

```bash
./gradlew publishToMavenLocal --stacktrace
```

## Stop Conditions

Stop and escalate when destructive actions, live release publication, or policy conflicts are required.

---
> Source: [szijpeter/webauthn-kotlin-multiplatform](https://github.com/szijpeter/webauthn-kotlin-multiplatform) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-05-03 -->
