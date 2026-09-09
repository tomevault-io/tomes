---
name: til-review
description: Review a TIL entry for style, accuracy, markdown lint compliance, README linkage, and wordlist coverage Use when this capability is needed.
metadata:
  author: jonasbn
---

For the given file:

1. Check writing style: direct and helpful voice, smooth transitions, no unnecessary filler.
2. Verify code examples are correct and that all file paths and commands are properly formatted.
3. Confirm a `## Resources and References` section exists with all links collected there, even if also mentioned in the body.
4. Run `markdownlint --config .markdownlint.json <file>` and report any violations.
5. Confirm the file has a matching entry in `README.md`; flag if it is missing.
6. Identify technical terms outside code blocks that are not in `.wordlist.txt` and suggest additions.

---
> Source: [jonasbn/til](https://github.com/jonasbn/til) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-06 -->
