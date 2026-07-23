---
name: orionjs
description: We have changes in the git uncommited files. Use when this capability is needed.
metadata:
  author: orionjs
---
We have changes in the git uncommited files.

You must follow the steps:
- commit the changes
- apply the `bunx changeset` using ALWAYS patch for all changes (but manually, since command is interactive)
- run the `bunx changeset version` command and ensure all changes are only PATCH (x.x.PATCH)
- do `git add .` and `git commit -m "changeset"` to commit the changeset
- get the OTP token using the command `op item get Npmjs --otp`
- publish the changes with `bun publish -r --otp=<code>`

You must make sure to:
- Execute all commands with permissions to access the files and internet for publish (without sandbox)
- Ensure all changes are PATCH, not minor, not major

* The only changes you need to worry about are the uncommited files

---
> Source: [orionjs/orionjs](https://github.com/orionjs/orionjs) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
