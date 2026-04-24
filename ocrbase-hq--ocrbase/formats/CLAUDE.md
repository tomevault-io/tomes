# ocrbase

> This is light weight, model agnostic API standardizes integrating visual language models (VLMs) across supported models.

## Usage

Add this to your project's CLAUDE.md to activate this skill:

```
Read and follow the instructions in .claude/skills/ocrbase/SKILL.md
```

Or copy the instructions below directly into your CLAUDE.md:

# ocrbase

This is light weight, model agnostic API standardizes integrating visual language models (VLMs) across supported models.

## ocrbase core

- parse() # turn document into text
- extract() # extract data from document into .json, supports structured outputs
- batchParse() # batch parse
- batchExtract() # batch extract

## ocrbase features

- s3 integration
- bullmq integration (parse/async, extract/async, batchParse, batchExtract)

## ocrbase models

- [glmocr](https://huggingface.co/zai-org/GLM-OCR)
- [paddleocr](https://huggingface.co/PaddlePaddle/PaddleOCR-VL)

---
> Source: [ocrbase-hq/ocrbase](https://github.com/ocrbase-hq/ocrbase) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:claude_md:2026-04-24 -->
