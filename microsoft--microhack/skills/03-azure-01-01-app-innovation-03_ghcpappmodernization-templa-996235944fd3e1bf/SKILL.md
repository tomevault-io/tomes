---
name: skill-name-kebab-case
description: >- Use when this capability is needed.
metadata:
  author: microsoft
---

<!--
  SKILL TEMPLATE — App Modernization knowledge package
  Copy to: <target-repo>/.github/skills/{{skill-name}}/SKILL.md
  The `description` is the routing contract — invest most effort there.
  Optional supporting files live next to this file (rulebooks, scripts, examples).
-->

# {{Skill Title — e.g. ".NET Framework → .NET 9 Migration Rules"}}

## Purpose

{{1–2 sentences: what knowledge this skill packages and what outcome it enables.}}

## Prerequisites

- {{e.g. "Assessment report (ASSESSMENT.md) exists"}}
- {{e.g. ".NET 9 SDK installed — verify with `dotnet --list-sdks`"}}

## Procedure

### Step 1 — {{e.g. "Detect the migration surface"}}

{{Concrete instructions. Prefer commands and decision tables over prose.}}

```{{lang}}
{{command or code example}}
```

### Step 2 — {{e.g. "Apply transformation rules"}}

| Source pattern | Target pattern | Notes |
|---|---|---|
| {{e.g. `WebForms .aspx`}} | {{e.g. `Razor Pages`}} | {{caveat}} |
| {{e.g. `javax.servlet.*`}} | {{e.g. `jakarta.servlet.*`}} | {{caveat}} |

### Step 3 — {{e.g. "Verify"}}

- [ ] {{verification item — e.g. "solution builds with zero warnings-as-errors"}}
- [ ] {{verification item — e.g. "all tests in CI suite pass"}}

## Common Pitfalls

- ⚠️ {{pitfall + how to avoid — e.g. "binding redirects are not honored in .NET 9; delete them and use the SDK-style project resolution"}}
- ⚠️ {{pitfall + how to avoid}}

## References

- {{Link to official migration guide / rulebook file in this folder}}
- {{e.g. `./rules/breaking-changes.md` (supporting file)}}

---
> Source: [microsoft/MicroHack](https://github.com/microsoft/MicroHack) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-08-09 -->
