# ⚙️ clang-format-for-linux-coding-style

<div align="center">

**一键让 `clang-format` 遵守 Linux 内核编码规范**  
[![License](https://img.shields.io/badge/license-GPL--2.0--only-blue.svg)](LICENSE)
[![clang-format](https://img.shields.io/badge/clang--format-10%2B-brightgreen)](https://clang.llvm.org/docs/ClangFormat.html)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)](https://github.com/JosiahBristow/clang-format-for-linux-coding-style/pulls)

</div>

---

## 📌 项目简介

Linux 内核有着严格的代码风格规范，但 `clang-format` 官方并未直接提供与之完全匹配的预设方案。  
本项目为你准备了**一份经过细致调优的 `.clang-format` 配置文件**，让你的 C/C++ 代码在格式化时**自动遵循 Linux 内核风格**。

只需一条命令，即可全局生效，告别手动调整缩进、括号、指针对齐等琐事。

---

## 🚀 快速启用

在终端执行以下命令，自动下载并部署配置（如已有配置会自动备份）：

```bash
[ -f ~/.clang-format ] && mv ~/.clang-format ~/.clang-format.bak
curl -fsSL https://raw.githubusercontent.com/JosiahBristow/clang-format-for-linux-coding-style/main/.clang-format -o ~/.clang-format
```

> 💡 **提示**：该配置将作为**用户级默认设置**，适用于所有项目。若某项目需要独立配置，只需在项目根目录放置自己的 `.clang-format` 即可覆盖。

---

## 🎯 为什么选择这个配置？

| 特性 | 说明 |
|------|------|
| ✅ **精准匹配内核风格** | 基于 Linux `Documentation/process/coding-style.rst` 逐项调校 |
| ✅ **Tab 缩进 + 8 空格宽度** | 符合内核主流偏好 |
| ✅ **大括号换行规则** | 函数换行，控制语句不换行，与内核代码完全一致 |
| ✅ **指针符号靠右** | 如 `int *ptr`，符合内核习惯 |
| ✅ **行宽 80 字符** | 保持经典终端可读性 |
| ✅ **不对 `#include` 自动排序** | 避免破坏原有依赖顺序 |

---

## 🔧 配置项详解

下表列出了关键定制参数及其含义：

| 配置项 | 取值 | 说明 |
|--------|------|------|
| `BasedOnStyle` | `LLVM` | 以 LLVM 风格为基础，再行覆写 |
| `UseTab` | `ForIndentation` | 缩进使用 Tab，对齐使用空格 |
| `TabWidth` | `8` | Tab 显示宽度为 8 空格 |
| `IndentWidth` | `8` | 缩进宽度（与 Tab 宽度一致） |
| `ColumnLimit` | `80` | 强制每行不超过 80 字符 |
| `AccessModifierOffset` | `-4` | 访问修饰符（public/private）缩进偏移 |
| `BreakBeforeBraces` | `Custom` | 启用自定义大括号换行策略 |
| `BraceWrapping.AfterFunction` | `true` | 函数左大括号另起新行 |
| `BraceWrapping.AfterControlStatement` | `false` | `if`/`for`/`while` 左大括号不换行 |
| `AllowShortFunctionsOnASingleLine` | `None` | 禁止任何短函数单行书写 |
| `AllowShortIfStatementsOnASingleLine` | `Never` | 禁止短 `if` 单行书写 |
| `PointerAlignment` | `Right` | 指针 `*` 紧贴变量名（如 `int *p`） |
| `SortIncludes` | `false` | 不自动重新排序头文件包含 |
| `Standard` | `c++03` | 使用 C++03 标准（兼容内核代码） |

> 📄 完整配置请参见仓库根目录下的 [`.clang-format`](.clang-format) 文件。

---

## 📝 使用示例

### 1️⃣ 格式化单个文件

```bash
clang-format -i kernel/sched/core.c
```

### 2️⃣ 批量格式化整个目录

```bash
find . -regex '.*\.\(c\|h\|cpp\|hpp\)' -exec clang-format -i {} \;
```

### 3️⃣ 集成到 VSCode

- 安装 `C/C++` 或 `Clang-Format` 扩展
- 在设置中启用 `Editor: Format On Save`
- 保存文件时即自动应用内核风格

### 4️⃣ Git 提交前自动格式化

在 `.git/hooks/pre-commit` 中添加：

```bash
#!/bin/sh
git diff --cached --name-only --diff-filter=ACM | grep -E '\.(c|h|cpp|hpp)$' | xargs clang-format -i
git add .
```
