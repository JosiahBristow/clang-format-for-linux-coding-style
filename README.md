# clang-format-for-linux-coding-style

本项目提供了一份专为 **Linux 内核编码风格（Linux Kernel Coding Style）** 定制的 `clang-format` 配置文件。  
将该配置文件放置于用户根目录下（`~/.clang-format`）后，`clang-format` 便会默认按照 Linux 内核的代码规范来格式化 C/C++ 代码。

## 快速开始

在终端中执行以下命令，即可一键下载并启用本配置：

```bash
[ -f ~/.clang-format ] && mv ~/.clang-format ~/.clang-format.bak
curl -fsSL https://raw.githubusercontent.com/JosiahBristow/clang-format-for-linux-coding-style/main/.clang-format -o ~/.clang-format
```

> **说明**：如果 `~/.clang-format` 已存在，该命令会先将其备份为 `~/.clang-format.bak`，再下载新配置。

## 配置特性

本配置文件基于 `LLVM` 风格，并针对 Linux 内核编码风格做了如下关键调整：

| 配置项 | 取值 | 说明 |
|--------|------|------|
| `BasedOnStyle` | `LLVM` | 以 LLVM 风格为基础进行定制 |
| `UseTab` | `ForIndentation` | 缩进使用 Tab，对齐使用空格（推荐） |
| `TabWidth` | `8` | Tab 显示宽度为 8 个空格 |
| `IndentWidth` | `8` | 缩进宽度为 8（与 TabWidth 一致） |
| `ColumnLimit` | `80` | 每行最大宽度 80 字符 |
| `AccessModifierOffset` | `-4` | 访问修饰符偏移（与内核风格一致） |
| `BreakBeforeBraces` | `Custom` | 自定义大括号换行规则 |
| `BraceWrapping.AfterFunction` | `true` | 函数大括号另起一行 |
| `BraceWrapping.AfterControlStatement` | `false` | `if`/`for`/`while` 大括号不换行 |
| `AllowShortFunctionsOnASingleLine` | `None` | 禁止短函数写在一行 |
| `AllowShortIfStatementsOnASingleLine` | `Never` | 禁止短 `if` 写在一行 |
| `PointerAlignment` | `Right` | 指针符号靠右（如 `int *ptr`） |
| `SortIncludes` | `false` | 不自动排序 `#include` |
| `Standard` | `c++03` | 使用 C++03 标准 |

完整的配置内容请参阅仓库中的 [.clang-format](.clang-format) 文件。

## 使用方式

### 1. 格式化单个文件

```bash
clang-format -i path/to/your/file.c
```

### 2. 格式化目录下所有 C/C++ 文件

```bash
find . -name "*.c" -o -name "*.h" -o -name "*.cpp" -o -name "*.hpp" | xargs clang-format -i
```

### 3. 在 VSCode 中启用

安装 `C/C++` 或 `Clang-Format` 扩展后，在设置中启用「Format On Save」即可在保存时自动格式化。

### 4. 在 Git 提交前自动格式化

可配合 `pre-commit` hook 使用，或直接运行：

```bash
git ls-files "*.c" "*.h" "*.cpp" "*.hpp" | xargs clang-format -i
```

## 注意事项

- **备份现有配置**：执行快速开始命令前，建议先备份原有的 `~/.clang-format`（命令已自动处理）。
- **clang-format 版本**：建议使用 **clang-format 10.0** 或更高版本，以确保所有配置选项被正确支持。
- **项目级配置**：如需为某个项目使用独立配置，可将 `.clang-format` 文件放置于项目根目录，其优先级高于 `~/.clang-format`。
- **内核风格参考**：Linux 内核官方编码风格文档见 [`Documentation/process/coding-style.rst`](https://www.kernel.org/doc/html/latest/process/coding-style.html)。
