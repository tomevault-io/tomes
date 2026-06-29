# la-resume

> Run after making React changes to catch issues early. Use when reviewing code, finishing a feature, or fixing bugs in a React project.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/la-resume/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# React Doctor

Run after making React changes to catch issues early. Use when reviewing code, finishing a feature, or fixing bugs in a React project.

Scans your React codebase for security, performance, correctness, and architecture issues. Outputs a 0-100 score with actionable diagnostics.

## Usage

```bash
npx -y react-doctor@latest . --verbose --diff
```

## Workflow

Run after making changes to catch issues early. Fix errors first, then re-run to verify the score improved.

---
> Source: [shubhamku044/la-resume](https://github.com/shubhamku044/la-resume) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-06-29 -->
