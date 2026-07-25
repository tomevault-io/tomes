---
name: image-gen
description: Generate images from text prompts via DashScope/Qwen. Use when creating, drawing, or illustrating images. Use when this capability is needed.
metadata:
  author: alibaba
---

# Image Generation

Run `scripts/generate_image.py` relative to this skill's directory.

```bash
python3 SKILL_DIR/scripts/generate_image.py -p "prompt text" -o output.png [-m model] [-s size]
```

Default model: `wanx2.1-t2i-turbo`. Also: `wanx2.1-t2i-plus`, `wanx-v1`. Size default `1024*1024`.

Requires env var `DASHSCOPE_API_KEY` (or `QWEN_API_KEY`).

---
> Source: [alibaba/anolisa](https://github.com/alibaba/anolisa) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-12 -->
