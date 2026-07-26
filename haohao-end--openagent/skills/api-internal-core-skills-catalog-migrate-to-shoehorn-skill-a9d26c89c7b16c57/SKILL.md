---
name: openagent
description: 这是一个把测试里的类型断言迁移到 shoehorn 的技能。 Use when this capability is needed.
metadata:
  author: Haohao-end
---
# migrate-to-shoehorn

这是一个把测试里的类型断言迁移到 shoehorn 的技能。

## 适用场景

- 代码库里有大量 `as` 断言
- 想把测试断言变得更类型安全
- 用户希望批量迁移，而不是手工逐个改

## 工作方式

1. 找出使用 `as` 的测试。
2. 识别适合 shoehorn 的断言位置。
3. 逐文件迁移，保持行为不变。

---
> Source: [Haohao-end/openagent](https://github.com/Haohao-end/openagent) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
