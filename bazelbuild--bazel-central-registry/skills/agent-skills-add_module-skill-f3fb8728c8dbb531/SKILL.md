---
name: add-module
description: >- Use when this capability is needed.
metadata:
  author: bazelbuild
---

# Add Module

This skill provides the exact procedure for scaffolding a new module version in the Bazel Central Registry (BCR).

## Prerequisites
Make sure you are at the root of the `bazel-central-registry` repository.

## Procedure

Copy this checklist and track progress:
- [ ] Step 1: Create the version directory under `modules/{module_name}/{version}`
- [ ] Step 2: Copy `MODULE.bazel`, `source.json`, and `presubmit.yml` from a previous version
- [ ] Step 3: Update the new version entry in `modules/{module_name}/metadata.json`

### 1. Create Directory
```bash
mkdir -p modules/{module_name}/{version}
```

### 2. Initialize Files
Copy `MODULE.bazel`, `source.json`, and `presubmit.yml` from a previous version to the newly created directory. Update version info as needed.

### 3. Update Metadata
Add the new version to `modules/{module_name}/metadata.json`.

---
> Source: [bazelbuild/bazel-central-registry](https://github.com/bazelbuild/bazel-central-registry) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
