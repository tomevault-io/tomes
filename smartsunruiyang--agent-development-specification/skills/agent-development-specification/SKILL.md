---
name: agent-development-specification
description: >- Use when this capability is needed.
metadata:
  author: SmartSunruiyang
---

# Agent Development Specification (ADS)

This skill installs a **project-startup governance system**: the agent rules, the upstream
documents, and the architecture that must exist *before* code, so that every later session —
yours or another agent's — works against a stable source of truth instead of free-styling on a
codebase nobody can fully see.

The full rationale lives in `references/spec.md` (the canonical, technology-agnostic spec).
Read it when you need depth on *why* a rule exists; this file tells you *what to do*.

## Prime directive: obey the rules you install

This skill's output is a set of hard constraints (`SELF_CONSTRAINTS.md`) and a practice guide.
You must follow them while running init — installing a rulebook you then violate is worse than
installing nothing. Concretely:

- **Version control from day 0.** No file gets generated before the repo is under version control.
- **Non-destructive, always.** Never overwrite a file the user has tuned. The scaffold script skips
  anything that exists; you do the same when filling content — read first, reconcile, never clobber.
- **Never decide architecture silently.** Module splits, dependency direction, naming rules, and MVP
  scope have long-term consequences. Propose, explain the trade-off, let the user choose. Park
  assumptions in the PRD's "假设与待澄清项" for sign-off.
- **One purpose per run.** init lands rules + docs. It does not refactor existing code or build features.

## The init workflow

> The skill's base directory (shown to you when this skill loaded) contains `scripts/`, `assets/`,
> and `references/`. Paths below are relative to it.

### Phase 0 — Orient & detect state

Determine which mode you're in before touching anything:

```
git status / ls -a               → is there a version-control repo?
ls the source tree               → is there existing application code?
ls .project.agents/ (or chosen)  → is there already an ADS scaffold (full or partial)?
```

| Repo? | Existing code? | Scaffold present? | Mode |
|---|---|---|---|
| no | no | no | **Greenfield** — fresh start |
| either | yes | no | **Retrofit** — see `references/retrofit.md` |
| either | either | yes (partial/full) | **Top-up** — fill only what's missing, never overwrite |

Tell the user which mode you detected and what you're about to do, then proceed.

### Phase 1 — Mechanical scaffold (deterministic)

1. **Version control.** If there's no repo, initialize one. If the working tree is **dirty**
   (uncommitted changes from prior work), STOP and ask whether to commit/stash first — do not pile
   the scaffold onto unrelated dirty changes (`SELF_CONSTRAINTS §A2/F1`).

2. **Decide the structural values AND the project facts**, and write a config:
   ```json
   {
     "PROJECT_NAME": "...", "SOURCE_DIR": "...", "TEST_DIR": "...", "include_uiux": true,
     "PROJECT_TYPE": "...", "TECH_STACK": "...", "ENTRY_POINT": "...",
     "BUILD_COMMAND": "...", "RUN_COMMAND": "...", "TEST_COMMAND": "..."
   }
   ```
   The script bakes all of these in deterministically (paths land in ARCHITECTURE §6; the project facts
   fill `CLAUDE.md` and `AGENTS.md` everywhere they appear). **Fill in every project fact you can — these
   are the entry-point files every future agent reads first, and a missing build command is a high-cost
   error.** Don't accept generic defaults: set `SOURCE_DIR`/`TEST_DIR` to the stack's real convention
   (detect them in retrofit; pick per-stack in greenfield — e.g. not "src" for a Go or Swift layout), and
   the commands to what actually builds/runs/tests this project. Set `include_uiux` to `false` for non-UI
   projects (CLI, library, backend service) so no UIUX references are generated. Agents dir defaults to
   `.project.agents/` and docs to `.project.agents/docs/context/` — keep these unless the user differs.

3. **Run the scaffold script** — it creates the tree, copies the static governance files, substitutes
   structural tokens, and **skips everything that already exists**:
   ```sh
   python3 <skill-dir>/scripts/scaffold.py --repo <repo-root> --config <config.json>
   ```
   Run with `--dry-run` first if you want to preview. Read its report: it lists created vs. skipped files.

4. **Zero-point commit** (greenfield / clean tree only): stage the new files and commit the skeleton as
   the reference point, e.g. `chore: scaffold agent-governance + doc skeleton (ADS Day 0)`. On a dirty
   existing repo, skip the auto-commit and tell the user to review and commit themselves.

After Phase 1 the repo has a complete, valid governance tree — even if you stop here, nothing is broken.
The upstream docs still contain `{{CONTENT}}` tokens and `<!-- ADS:FILL -->` markers: those are Phase 2's job.

### Phase 2 — Guided interview (fills the real content)

Walk the user through `references/interview-flow.md` — the operational version of the spec's
Steps 1–7 (requirements → domain model → modules → dependency DAG → roadmap → conventions). For each
step: ask, write the answer into the corresponding doc (replacing tokens and removing the `ADS:FILL`
comments), show the user, move on. Key discipline:

- **In retrofit mode**, read `references/retrofit.md` first — you draft ARCHITECTURE from the existing
  code (prefer CodeGraph MCP if available) and present it for correction, rather than asking from scratch.
- **Pace it and scale it.** One step at a time. A small project gets few modules and milestones; don't
  manufacture eight layers for a 200-line tool. The card/section *format* is fixed; the *volume* isn't.
- **The "不负责" line is the test of a module.** If you can't write what a module does NOT do, its
  responsibility isn't crisp — re-split before moving on.
- **Verify the DAG is acyclic by hand.** A cycle means two modules are tangled; resolve it now.
- **Finish `CLAUDE.md` and `AGENTS.md` — do not leave them as skeletons.** It is tempting to lavish
  attention on PRD/ARCHITECTURE (the interesting docs) and abandon these two, but they are the FIRST
  files every future agent reads. After the interview, fill their remaining tokens and `ADS:FILL`
  sections — the architecture/module overview, conventions summary, test framework, and anything the
  config didn't already supply — and `CONVENTIONS.md`/`UIUX.md` too. A scaffold whose entry-point files
  still say `{{TECH_STACK}}` has failed at its one job.

### Phase 3 — Finalize & hand off

- **Completion gate (run before committing).** Grep the whole scaffold for anything left unfilled and
  resolve every hit — fill it with real content, or delete the line if it genuinely doesn't apply:
  ```sh
  grep -rn -e '{{[A-Z0-9_]*}}' -e 'ADS:FILL' <agents-dir>/   # expect: no output
  ```
  A surviving `{{TOKEN}}` or `ADS:FILL` marker means the doc is half-written. The one exception is
  `VIBECODING_GUIDE.md` §8's current-phase note, which you should fill but is low-stakes. Do not commit
  with residue in `CLAUDE.md`, `AGENTS.md`, `PRD.md`, `ARCHITECTURE.md`, `CONVENTIONS.md`, or `UIUX.md`.
- Resolve or explicitly defer each item in the PRD's "假设与待澄清项" with the user.
- Update `VIBECODING_GUIDE.md` §8 "本项目当前阶段" to the real current state.
- Commit the filled upstream docs, e.g. `docs: define PRD/ARCHITECTURE/ROADMAP/CONVENTIONS (ADS init)`.
- Offer Step 7 (derived docs — implementation spec, asset checklist) only if the project needs them.
- Summarize: what was created, what's still `ADS:FILL`/deferred, and the recommended first milestone.

## Language of generated docs

Default to the user's working language for the governance files and doc skeletons; the shipped templates
are written in Chinese to match the canonical spec, so render them in another language if the project's
working language differs. Keep `AGENTS.md` in **English** by convention — it's the cross-vendor contributor
guide that non-Claude agents (e.g. Codex) read.

## Resources

- `references/spec.md` — the canonical universal spec (the full "why"; read for depth).
- `references/interview-flow.md` — operational Step 1–7 interview guide (Phase 2).
- `references/retrofit.md` — reverse-engineering a draft architecture from existing code.
- `assets/templates/` — the files written into the repo: governance (`SELF_CONSTRAINTS.md`,
  `VIBECODING_GUIDE.md`, `CLAUDE.md`, `AGENTS.md`, `settings.json`, `log-README.md`, `gitignore-base`)
  and doc skeletons under `docs/` (`PRD`, `ARCHITECTURE`, `ROADMAP`, `CONVENTIONS`, `UIUX`).
- `scripts/scaffold.py` — deterministic, idempotent, non-destructive tree + static-file creator.

## Token conventions inside the templates

- `{{STRUCTURAL}}` tokens (paths, doc names, `PROJECT_NAME`) — substituted by the scaffold script.
- `{{CONTENT}}` tokens (e.g. `{{BUILD_COMMAND}}`, `{{MODULE_OVERVIEW}}`, `{{FEATURE_NAME}}`) — you fill
  these during the interview.
- `<!-- ADS:FILL ... -->` — guidance for a section you must complete; delete the comment once filled.

---
> Source: [SmartSunruiyang/Agent-development-specification](https://github.com/SmartSunruiyang/Agent-development-specification) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-18 -->
