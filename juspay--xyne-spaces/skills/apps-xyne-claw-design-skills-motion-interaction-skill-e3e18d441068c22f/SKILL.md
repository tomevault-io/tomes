---
name: motion-interaction
description: Add purposeful interaction and motion to HTML designs, including state transitions, feedback, navigation, disclosure, and reduced-motion behavior. Use when this capability is needed.
metadata:
  author: juspay
---

# Motion and interaction

Motion should explain state change, not delay the user.

- Use short transitions for hover, focus, selection, expansion, and feedback.
- Keep entrance animation rare and subordinate to content; stagger only a few
  meaningful items.
- Give every action immediate feedback and preserve state consistently.
- Prevent accidental form submission and repeated destructive actions.
- Use transforms and opacity for smooth animation; avoid layout-thrashing loops.
- Under `prefers-reduced-motion: reduce`, remove nonessential movement and keep
  state changes understandable.

Test the actual interaction after implementation. A visually convincing button
that does nothing is a defect, not a mockup detail.

---
> Source: [juspay/xyne-spaces](https://github.com/juspay/xyne-spaces) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-20 -->
