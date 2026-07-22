---
name: 60s
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# 60s 聚合信息查询技能

一站式日常信息查询，覆盖新闻、天气、热搜、金融、娱乐等 17 个工具。

## 工具速查

根据用户意图选择对应工具：

| 用户说… | 用这个工具 |
|---------|-----------|
| 今天有什么新闻 / 60s 看世界 | `60s_news` |
| XX 天气怎么样 | `weather` |
| 微博热搜 | `weibo_hot` |
| 知乎热搜 | `zhihu_hot` |
| 抖音热搜 | `douyin_hot` |
| 今日头条 | `toutiao_hot` |
| 金价多少 | `gold_price` |
| 油价多少 | `fuel_price` |
| 美元汇率 / 人民币兑日元 | `exchange_rate` |
| 翻译一下 XX | `translate_60s` |
| 来句一言 / 每日一句 | `hitokoto` |
| 摸鱼日历 / 今天摸鱼 | `moyu` |
| KFC 文案 / 疯狂星期四 | `kfc` |
| 来个段子 | `duanzi` |
| 历史上的今天 | `history_today` |
| 查 IP / 我的 IP | `ip_query` |
| Bing 壁纸 / 每日壁纸 | `bing_image` |

## 易错点

1. **weather 需要城市名参数**，用户没说城市时需要先确认。
2. **exchange_rate 需要币种参数**，如 USD、JPY、EUR 等。
3. **translate_60s 是简易翻译**，对于复杂翻译任务应建议使用专业翻译工具。
4. **热搜类工具不需要参数**，直接调用即可获取当前热搜列表。

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
