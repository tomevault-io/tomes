---
name: sync-review
description: >- Use when this capability is needed.
metadata:
  author: thun-res
---

# 全仓同步审计

代码定义行为,`doc/` 定义产品与架构语义;Doxygen、绑定、测试、示例、
构建打包、`.github`、Agent 索引和变更摘要均须与对应事实同步。

## 1. 功能路由

只加载当前审计需要的分册:

| 功能 | 必读分册 |
|---|---|
| 确定全量/增量范围和事实基准 | [CHANGE-SCOPE.md](references/CHANGE-SCOPE.md) |
| 核对 API、绑定、文档、测试与示例 | [API-SURFACES.md](references/API-SURFACES.md) |
| 核对 CMake、Conan、Android.bp、vcpkg、packup 与安装发布链 | [BUILD-PACKAGING-SURFACES.md](references/BUILD-PACKAGING-SURFACES.md) |
| 核对图、Wiki、选项、索引与版本等易漂移项 | [CROSS-CHECKS.md](references/CROSS-CHECKS.md) |
| 核对 `.github` 工作流、脚本、模板、Docker、Wiki 与治理细节 | [GITHUB-SURFACES.md](references/GITHUB-SURFACES.md) |
| 分类发现、修复授权、并行审计与报告 | [REPORTING.md](references/REPORTING.md) |

## 2. 执行边界

- 全量审计覆盖全部分册和 `.github` 全部文件;增量审计按变更面加载
  对应功能,但不得漏掉直接派生面。
- 除非用户明确要求修复,否则只读审计,不修改仓库内容;只有明确要求
  落盘时才写报告。
- 每项结论必须同时给出事实侧和派生侧证据;不适用项说明原因。
- 已落盘时最终回复摘要结论并给出路径;否则直接给出审计结论。

---
> Source: [thun-res/vlink](https://github.com/thun-res/vlink) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-09-13 -->
