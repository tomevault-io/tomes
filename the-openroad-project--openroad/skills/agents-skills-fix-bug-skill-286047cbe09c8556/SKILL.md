---
name: fix-bug
description: > Use when this capability is needed.
metadata:
  author: The-OpenROAD-Project
---

# Fix OpenROAD Bug

You are fixing a bug related to **$ARGUMENTS**.

## 1. Understand the bug

If `$ARGUMENTS` is a GitHub issue number:
```bash
gh issue view $ARGUMENTS --repo The-OpenROAD-Project/OpenROAD \
  --json title,body,labels,comments
```

Extract from the issue:
- **Error string** (e.g. `GPL-0305`, `DRT-0001`) -- search for the exact message ID
- **Module** -- infer from labels or error prefix
- **Steps to reproduce** -- look for attached scripts, Tcl commands, or tarballs
- **Stack trace** -- if a crash, identify the faulting function

If `$ARGUMENTS` is an error code, search for it directly:
```bash
grep -rn "ERROR_CODE" src/MODULE/src/
```

## 2. Trace the root cause

Follow OpenROAD's "trace bugs upstream" principle: find where the bad
data is **created**, not where it is **reported**.

1. Find the error message source:
   ```bash
   grep -rn "ERROR_ID" src/
   ```
2. Read the surrounding code to understand the condition that triggers it
3. Trace the data flow backward -- who sets the offending value?
4. Identify the actual bug location (often in a different function/file
   from where the error is reported)

**Critical constraint**: Never modify files under `src/sta/`. OpenSTA is
managed upstream. If the root cause is in OpenSTA, report this finding
instead of patching it.

## 3. Implement the fix

Follow the coding practices in `docs/agents/coding.md`. Pay special
attention to `int64_t` for area calculations and removing unreachable
code after `error()` or `throw`.

## 4. Create regression test

Every bug fix needs a test that reproduces the exact failure mode from
the issue (same error code, same stack frame, same condition) so a
future regression is caught immediately.

Use the **add-test** skill (`.agents/skills/add-test/SKILL.md`) for the
full workflow: writing the test, generating golden files, and
registering in both CMake and Bazel.

## 5. Format and commit

```bash
# Format changed C++ files (NEVER format src/sta/* or *.i files)
clang-format -i <changed-cpp-files>

# Stage and commit with DCO sign-off
git add <changed-files>
git commit -s -m "MODULE: fix BRIEF_DESCRIPTION

Fixes #ISSUE_NUMBER"
```

## 6. Verify

- [ ] Test passes: `cd src/MODULE/test && ./regression -R TEST_NAME`
- [ ] No unintended changes: `git diff HEAD`
- [ ] Test registered in both CMake and Bazel
- [ ] No `src/sta/` files modified
- [ ] C++ files formatted with clang-format
- [ ] Commit is signed off (`-s`)

---
> Source: [The-OpenROAD-Project/OpenROAD](https://github.com/The-OpenROAD-Project/OpenROAD) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
