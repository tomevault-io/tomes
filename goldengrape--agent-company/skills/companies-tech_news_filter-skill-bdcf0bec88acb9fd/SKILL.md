---
name: tech-news-filter
description: 科技新闻筛选公司。聚合顶级科技媒体RSS新闻源，执行底层技术情报过滤，翻译为简体中文，生成每日硬核科技新闻报告。 Use when this capability is needed.
metadata:
  author: goldengrape
---

# Tech News Filter — 科技新闻筛选公司

## Overview
Tech News Filter 是一个底层技术情报分析公司。其核心使命是从海量科技新闻中提取具有架构级、机制级价值的硬核信息，过滤一切公关噪音、政治化叙事和碎片化内容，为高密度信息消费者提供每日精炼情报。

## Components

### 1. 岗位 (Posts) - `POSTS.md`
定义公司内的四个专业岗位：
- **RSS采集翻译员**: 从指定媒体源抓取并翻译新闻
- **首席情报筛选官**: 执行核心 PASS/BLOCK 过滤逻辑
- **情报合成员**: 撰写冷峻学术化的每日报告
- **质量审计员**: 验证过滤准确性和报告质量

### 2. 公文 (Docs) - `DOCS_SCHEMA.md`
定义公司专用公文：
- 每日采集任务单 (Input)
- 原始新闻清单 (Intermediate)
- 筛选后新闻清单 (Intermediate)
- 每日新闻报告 (Output)
- 质量审计报告 (Verification)

### 3. 流程 (Workflows) - `WORKFLOWS.md`
定义"每日新闻筛选"的标准流程：
- 采集翻译 → 情报筛选 → 报告合成 → 质量审计 → 归档发布

## Usage
```bash
# 运行每日新闻筛选（从 workspace/tasks 读取任务）
nanobot company run --name tech_news_filter

# 指定任务文件运行
nanobot company run --name tech_news_filter --task ./my_task.md

# 传入任务字符串运行
nanobot company run --name tech_news_filter --task "筛选今日AI领域新闻"
```

---
> Source: [goldengrape/Agent-company](https://github.com/goldengrape/Agent-company) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-20 -->
