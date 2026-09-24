---
name: title-card-image
description: Render a static title / ending card PNG with Pillow. Centered headline + optional subtitle on a solid-colour background. Uses managed or platform CJK fonts with glyph verification and fails actionably instead of rendering tofu. Pure deterministic, no LLM, no network. Used by meta-short-drama for opening and closing cards. Use when this capability is needed.
metadata:
  author: TokenRhythm
---

# title-card-image

Renders a centered-text PNG suitable for a cover / ending card before
animating into a clip with `video-still-animator`.

## Inputs (`with:`)

| key | required | default | notes |
|---|---|---|---|
| `text` | yes | — | Headline text. Auto-wraps at ~10 chars per line for CJK. |
| `output` | yes | — | Output `.png` path. |
| `subtitle` | no | `""` | Smaller line beneath the headline. |
| `background` | no | `#101018` | Hex color `#RRGGBB`. |
| `text_color` | no | `#ffffff` | Headline color. |
| `font_size` | no | `96` | Headline font size in pixels. |
| `subtitle_size` | no | `36` | Subtitle font size in pixels. |
| `width` | no | `720` | Output width in pixels. Match the merge pipeline. |
| `height` | no | `1280` | Output height. 720x1280 = 9:16. |
| `font` | no | `""` | Optional `.ttf`, `.otf`, or `.ttc` path. Must contain the requested CJK glyphs. |

## Output

Prints the absolute path of the written PNG on stdout. The PNG is RGB
(no alpha), JPEG-quality-equivalent file ~30-80 KB depending on text
length.

## Font fallback

Resolution order is `--font`, the managed media directory from
`OPENSQUILLA_MEDIA_FONTS_DIR`, user font directories, then platform defaults:
Microsoft YaHei / SimHei / DengXian on Windows; PingFang / Hiragino Sans GB /
STHeiti / Songti on macOS; Noto CJK / Source Han / WenQuanYi on Linux. Font
collection files (`.ttc`/`.otc`) are supported. Before drawing, the renderer
compares requested non-ASCII glyphs with the font's missing-glyph signature. A font
that would produce tofu is skipped. If no compatible scalable font exists, the
step fails with an actionable `--font` / `OPENSQUILLA_MEDIA_FONTS_DIR` message
for CJK or other non-ASCII text; it never silently emits tiny bitmap squares.
Pure ASCII cards remain available on minimal systems through Pillow's built-in
font when no scalable font is installed.

## Limits

- No alpha / transparency.
- No rich text styling (italic / drop-shadow / gradient). For richer
  cards, generate a real image via `nano-banana-pro` instead.
- Headline wrap is character-count-based for CJK and whitespace-based
  for ASCII; mixed strings break at the CJK character count.

---
> Source: [TokenRhythm/opensquilla](https://github.com/TokenRhythm/opensquilla) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-16 -->
