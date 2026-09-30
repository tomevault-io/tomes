---
name: edit-deployed-website
description: 1. Treat the Desktop Edit entry's `node_id` and workspace `source_path` as trusted: the source is Use when this capability is needed.
metadata:
  author: MiniMax-AI
---

# Edit Deployed Website

1. Treat the Desktop Edit entry's `node_id` and workspace `source_path` as trusted: the source is
   already available in the workspace. If `source_path` is missing, ask the user to reopen the site
   from its page's Edit action and stop. Do not use `node_id` to download anything, and do not use
   shell `curl` or an OSS URL. Do not add or invoke a checkout Tool.
2. Modify the existing project. Reuse its lockfile and package manager, run the affected tests, then
   run its real build command. Identify the built output and verify a regular `index.html` at its
   root.
3. Before publishing, explain that this updates the existing site in place to preserve the original
   node and its primary and alias URLs. State that `source_path` is uploaded to private cloud
   storage and there is currently no secrets scanner; ask the user to confirm `source_path` contains
   no secrets, then obtain explicit publication confirmation.
4. Call the existing `website_deploy({ node_id, path, source_path, project_name })` tool only after
   confirmation. Do not call republish and do not automatically revoke or delete the existing
   website.
5. Follow the existing `website_deploy` delivery format using only the tool-returned URL and
   `node_id`. Never guess or hand-write `cover`; let Runtime's trusted projection control final
   `node_id`/`cover`. Surface a tool failure as returned.

---
> Source: [MiniMax-AI/minimax-code](https://github.com/MiniMax-AI/minimax-code) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-28 -->
