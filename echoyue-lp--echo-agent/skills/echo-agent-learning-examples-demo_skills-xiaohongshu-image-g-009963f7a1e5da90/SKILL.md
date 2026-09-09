---
name: xiaohongshu-image-generator
description: 根据小红书文章内容自动生成配图。使用PIL将文章标题、副标题、内容生成在图片上，适合小红书笔记配图。 Use when this capability is needed.
metadata:
  author: EchoYue-lp
---

# 小红书配图生成器

根据文章内容自动生成小红书风格的配图。

## 使用方法

调用 `scripts/generate_cover.py` 脚本：

```bash
python3 scripts/generate_cover.py "标题" "副标题" "内容第一行\n内容第二行\n内容第三行"
```

## 参数说明

- 第1个参数：标题（必填）
- 第2个参数：副标题（可选，默认空）
- 第3个参数：正文内容，多行用\n分隔（可选）
- 第4个参数：输出图片路径（可选，默认 `xhs_cover.jpg`）

## 输出

图片保存为 `xhs_cover.jpg`

## 示例

```bash
python3 scripts/generate_cover.py "今日分享" "打卡第二天" "今天天气很好\n心情也不错\n继续加油！"
```

---
> Source: [EchoYue-lp/echo-agent](https://github.com/EchoYue-lp/echo-agent) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-08 -->
