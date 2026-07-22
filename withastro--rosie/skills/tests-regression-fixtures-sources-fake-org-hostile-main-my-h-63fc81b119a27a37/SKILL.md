---
name: my-hostile-skill
description: Use when working with a skill with invisible chars and comments. Used to test sanitize_skill.
metadata:
  author: withastro
---

# my-hostile-skill

<!-- skill authors keep their comments; this should survive a skill install -->

This skill body contains a zero-width joiner between rosie‍good (U+200D
inserted) that must be stripped on install.

It also has a Trojan Source bidi override here: ‮reversed‬ which must vanish.

End of skill.

---
> Source: [withastro/rosie](https://github.com/withastro/rosie) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
