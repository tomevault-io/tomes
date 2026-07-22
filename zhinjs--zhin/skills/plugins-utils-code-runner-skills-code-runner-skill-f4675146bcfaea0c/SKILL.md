---
name: code-runner
description: >- Use when this capability is needed.
metadata:
  author: zhinjs
---

# 在线代码执行技能

通过 glot.io API 在隔离沙箱中执行代码，不影响本地环境。

## 使用方式

调用 `run_code` 工具，传入 `language`（语言标识）和 `code`（代码内容）。

**支持语言：** python, javascript, typescript, go, rust, java, c, cpp, ruby, php

**Example:**
```
用户: 帮我算一下 1 到 100 的和
→ run_code(language="python", code="print(sum(range(1, 101)))")
```

## 限制

- 代码长度上限 **10000 字符**
- 执行超时 **30 秒**
- 无法访问网络和文件系统（沙箱隔离）
- 不支持交互式输入（stdin）

## 易错点

1. **language 参数必须是上面列出的标识符**，不接受中文或全名（如用 `python` 不用 `Python3`）。
2. **C 和 C++ 是不同的 language 值**：`c` 和 `cpp`。
3. **代码需要有输出语句**（print/console.log/fmt.Println 等），否则返回为空。

---
> Source: [zhinjs/zhin](https://github.com/zhinjs/zhin) — distributed by [TomeVault](https://tomevault.io).
<!-- tomevault:4.0:skill_md:2026-07-09 -->
