---
name: inbox-add-reaction
description: Add a reaction to a GitHub issue or pull request Use when this capability is needed.
metadata:
  author: microsoft
---

# Add Reaction

Add an emoji reaction to an issue or pull request.

## Command

```
gh api --method POST /repos/{owner}/{repo}/issues/{number}/reactions -f content={reaction}
```

## Available reactions

- `+1` (thumbs up 👍)
- `-1` (thumbs down 👎)
- `laugh` (😄)
- `confused` (😕)
- `heart` (❤️)
- `hooray` (🎉)
- `rocket` (🚀)
- `eyes` (👀)

Replace `{owner}`, `{repo}`, `{number}`, and `{reaction}` with the appropriate values. Note: this endpoint works for both issues and pull requests (PRs are issues in GitHub's API).

---
> Source: [microsoft/vscode-team-kit](https://github.com/microsoft/vscode-team-kit) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
