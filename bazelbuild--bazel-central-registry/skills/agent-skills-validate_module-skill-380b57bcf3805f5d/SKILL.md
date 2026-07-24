---
name: validate-module
description: >- Use when this capability is needed.
metadata:
  author: bazelbuild
---

# Validate Module

This skill provides the exact procedure for validating and iterating on a module version in the Bazel Central Registry (BCR).

## Procedure

Copy this checklist and track progress:
- [ ] Step 1: Run validation checks
- [ ] Step 2: Update source integrity
- [ ] Step 3: Check overlay and patch consistency

### 1. Validate
Run the local BCR validation tool:
```bash
bazel run //tools:bcr_validation -- --check {module_name}@{version}
```

### 2. Update Integrity
Generate or update the SHA-256 integrity hash:
```bash
bazel run //tools:update_integrity -- {module_name} --version={version}
```

### 3. Overlay vs Patches
- **overlay/**: Add or overwrite files. Requires `bazel_compatibility >= 7.2.1` in `MODULE.bazel`.
- **patches/**: Modify existing upstream source files using `.patch` files.
- **README.md**: Add a README.md if the purpose of overlay or patch files are
  not obvious.

### 4. Consistency Check
- If the source archive doesn't contain a MODULE.bazel, `modules/{module_name}/{version}/MODULE.bazel` should not exist.
- Otherwise, ensure that `modules/{module_name}/{version}/MODULE.bazel` matches the source archive's version exactly. Use an overlay or patch if they differ.

---
> Source: [bazelbuild/bazel-central-registry](https://github.com/bazelbuild/bazel-central-registry) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
