---
name: fiori-tools-samples
description: **Trigger:** `/km-review [<file-path> | --latest] [--fix] [--score-only] [--ai-only]` Use when this capability is needed.
metadata:
  author: SAP-samples
---
# KM Review Skill

**Trigger:** `/km-review [<file-path> | --latest] [--fix] [--score-only] [--ai-only]`

**Purpose:** Audit a Markdown file against SAP KM standards. Optionally apply safe fixes.

---

## Steps

### 1. Parse Arguments

Extract from `args`:
- `file_path` — path to a `.md` file (relative to repo root or absolute). Required unless `--latest` is passed.
- `--latest` flag — if present, derive `file_path` from the most-recently changed `.md` file in git.
- `--fix` flag — if present, apply safe fixes after review.
- `--score-only` flag — if present, display only the quality score and exit.
- `--ai-only` flag — if present, skip the docs-linter step and run AI review only.

**If `--latest`:**
```bash
git diff --name-only HEAD~1 -- '*.md'
```
If multiple files changed, review each in order (most recently changed first). If no `.md` files changed in `HEAD~1`, try staged changes:
```bash
git diff --cached --name-only -- '*.md'
```
If still nothing, tell user: `No changed .md files found in latest commit or staged changes.` and stop.

**If neither file path nor `--latest`:** tell user `Usage: /km-review <file-path> [--fix]` or `/km-review --latest [--fix]` and stop.

### 2. Validate the File

- Verify the file exists.
- Confirm it has a `.md` extension.
- Read the full file content.

### 3. Run Markdown Lint

```bash
./scripts/lint-markdown.sh <file-path>
```

Capture output. If the script does not exist or fails, note it and continue to the next step.

### 4. Optional: Run docs-linter (skip if `--ai-only`)

```bash
node docs-linter/src/cli.js validate <file-path> --json
```

If the command succeeds, collect the JSON findings for merging with the AI review. If it fails or the tool is not present, continue without it.

### 5. Load KM Rules

Read both rule sources in full:
- `prompts/km-doc-review.md` — full AI review prompt and output schema
- `docs/km-style-guide.md` — canonical style guide

### 6. AI Review

Apply all rules from both files to the file contents. Produce a structured review with:

- **structural_review** — heading hierarchy, section ordering, missing sections; severity: info/minor/major/critical
- **formatting_issues** — list markers, code fences, broken syntax
- **duplication_findings** — repeated content with consolidation recommendations
- **clarity_readability_review** — active voice, tense, word replacements (will→present, might→may, etc.)
- **consistency_validation** — SAP terminology, casing, inline code rules
- **quality_score** — overall 1–10 with breakdown (structure, clarity, maintainability, developer usability) and rationale

For each finding include: severity, location (section + approximate line), what's wrong, suggested fix, and whether it is safe to auto-fix.

If docs-linter findings are available, merge and deduplicate them with AI findings — do not report the same issue twice.

### 7. Output Review

**If `--score-only`:** display only the quality score and breakdown, then stop.

Otherwise, print the structured review clearly. Group by category. Lead with critical and major findings.

End with:
```text
Quality score: X/10
Critical: N  Major: N  Minor: N  Info: N
```

If `--fix` was not passed, append:
```text
To apply safe fixes, run: /km-review <file-path> --fix
```

### 8. If `--fix` Flag

After printing the review, apply **safe** fixes only — changes that cannot alter technical meaning:

- Replace `*` list markers with `-`
- Replace `—` or `→` in list items with `:`
- Fix heading capitalization to Chicago title case
- Replace banned words: `simply`, `currently` (standalone), `please `, `In order to` → `To`, `It is also possible to` → `You can also`, `might` → `may`, `including` → `which includes/include`, ` via ` → ` using `, `below` → `following` (document references only), `will ` (future tense in instructions) → present tense equivalent where unambiguous
- Fix SAP terminology from the table in `docs/km-style-guide.md`
- Fix `npm` → `` `npm` `` in prose, `devDependencies` → `` `devDependencies` `` in prose
- Fix `JSON` / `GUI` capitalisation in prose
- Fix `i.e.` → `that is,` and `e.g.` → `for example,`
- Remove `$` prompt from code block commands
- Fix list markers to dashes

Do **not** auto-fix: rewritten sentences, link text changes, structural reordering, content additions, or anything requiring judgment about technical meaning.

Write the fixed file back. Report what was changed.

## Error Handling

- File not found: `Error: File not found: <file-path>`
- Not a markdown file: `Error: Only markdown files (.md) are supported`
- No changed files (--latest): `No changed .md files found in latest commit or staged changes.`
- docs-linter missing or failing: continue with AI-only review, note in output
- Auto-fix fails: `Error: Failed to apply fixes. File unchanged. Findings available above.`

---
> Source: [SAP-samples/fiori-tools-samples](https://github.com/SAP-samples/fiori-tools-samples) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
