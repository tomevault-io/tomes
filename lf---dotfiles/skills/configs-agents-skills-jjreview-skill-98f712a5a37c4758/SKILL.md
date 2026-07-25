---
name: jjreview
description: Review a Jujutsu change in depth using pr-review-toolkit plus architectural analysis Use when this capability is needed.
metadata:
  author: lf-
---

First, show the change to review. Run `jj show <revset> --git`, where
`<revset>` is `$ARGUMENTS` if the user supplied one, otherwise `@-`.
Write the command with a literal revset (e.g. `jj show @- --git`).

Then review that change systematically and in depth.

For the code itself, use the pr-review-toolkit. But also independently think
about higher-level architectural concerns and the negative space — what do we
need to update that we missed?

---
> Source: [lf-/dotfiles](https://github.com/lf-/dotfiles) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-25 -->
