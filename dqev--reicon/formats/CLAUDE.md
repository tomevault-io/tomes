# reicon

> Scans your Next.js codebase for patterns that drive up your Vercel bill, focusing on compute duration, function invocations, and bandwidth optimization.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/reicon/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# Vercel Doctor

Scans your Next.js codebase for patterns that drive up your Vercel bill, focusing on compute duration, function invocations, and bandwidth optimization.

## Usage

\`\`\`bash
npx -y vercel-doctor@latest . --verbose --diff
\`\`\`

## Workflow

Run after making changes to catch cost-heavy patterns early. Focus on fixing issues that reduce function execution time and invocations first.

---
> Source: [dqev/reicon](https://github.com/dqev/reicon) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-09-23 -->
