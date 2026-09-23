---
name: merge-main-to-nightly
description: >- Use when this capability is needed.
metadata:
  author: dotnet
---

# Workflow: Merge main to nightly

This should be done as soon as possible after a new .NET release (same day).

1. Determine the release name. Run `pwsh eng/Get-ReleaseBranches.ps1` to find the latest release branch. The most recently created branch corresponds to the current release.
2. Fetch changes from the dotnet/dotnet-docker `main` and `nightly` branches.
3. Create a new branch based off of the `nightly` branch, called `merge-main-to-nightly-$releaseName`.
4. Merge main into your working branch with `git merge $remote/main`. If there are conflicts, invoke the `resolving-conflicts` skill.
5. Stop and confirm the changes with the user. Ask them to review the changes and wait for confirmation to proceed.
6. Submit the PR using the [template](./reference/pull-request-template.md).

---
> Source: [dotnet/dotnet-docker](https://github.com/dotnet/dotnet-docker) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-17 -->
