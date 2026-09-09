---
name: create-vercel-ai-issue
description: Create a well-formed GitHub issue in vercel/ai using the gh CLI. Use when reporting an AI SDK bug or preparing an issue body that contains logs, code blocks, versions, reproduction steps, and shell-sensitive text. Use when this capability is needed.
metadata:
  author: FranciscoMoretti
---

# Create a vercel/ai issue

1. Confirm `gh auth status` and inspect `vercel/ai` before writing.
2. Prepare a focused issue with sections for the problem, exact error, package
   versions, minimal reproduction, expected behavior, and actual behavior.
3. Put complex Markdown in a temporary body file so shell interpolation cannot
   alter backticks or code blocks.
4. Run `gh issue create -R vercel/ai --title "<title>" --body-file <file>`.
5. Return the created issue URL.

Do not create the external issue unless the user has authorized that write.

---
> Source: [FranciscoMoretti/chat-js](https://github.com/FranciscoMoretti/chat-js) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-09 -->
