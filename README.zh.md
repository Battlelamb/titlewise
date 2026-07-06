<div align="center">

<img src="assets/banner.png" alt="titlewise - 为 Claude Code 对话命名、加标题和打标签" width="100%">

**一个 [Claude Code](https://code.claude.com) 技能，把任意对话变成日后真正能找得到的标题。**

[![Release](https://img.shields.io/github/v/release/Battlelamb/claude-code-conversation-titler?style=flat-square&color=2dcd7a&logo=github&label=release)](https://github.com/Battlelamb/claude-code-conversation-titler/releases)
&nbsp;[![Stars](https://img.shields.io/github/stars/Battlelamb/claude-code-conversation-titler?style=flat-square&color=8b5cf6&logo=github)](https://github.com/Battlelamb/claude-code-conversation-titler/stargazers)
&nbsp;[![License](https://img.shields.io/badge/license-MIT-22d3ee?style=flat-square)](LICENSE)
&nbsp;[![Claude Code](https://img.shields.io/badge/Claude_Code-skill_%26_plugin-ec4899?style=flat-square)](https://code.claude.com)
&nbsp;[![PRs welcome](https://img.shields.io/badge/PRs-welcome-2dcd7a?style=flat-square)](https://github.com/Battlelamb/claude-code-conversation-titler/pulls)

<br>

<img src="assets/demo.gif" alt="titlewise 演示 - 交互式对话标题生成" width="760">

<sub>[English](README.md) · [Türkçe](README.tr.md) · **中文**</sub>

</div>

---

## 概述

**titlewise** 是一个交互式 Claude Code 技能，它读取你当前的对话，提出简洁、结构良好的**标题** - 长或短、带或不带日期，使用你自己的语言、英语或中文 - 并附带一段简短描述和搜索标签。你挑选喜欢的一个，将其设为对话标题。

可以把它看作 Claude Code 的**对话标题生成器**：几秒钟内为任意会话命名、加标题或打标签，让过往对话日后易于查找。

**仅建议**：它只提出建议，由你来应用。它绝不会改动你的会话或记录。

## 特性

| | |
|---|---|
| 🎛️ **交互式** | 生成前会询问你想要的标题方式（语言、长度、日期、风格） |
| 🌍 **多语言** | 对话语言（自动检测）、英语或中文 - 可选一种或多种 |
| 📏 **13+ 种变体** | 长 / 中 / 短，带 / 不带日期，slug、关键词、方括号、月份、结果、表情 |
| 📝 **不止是标题** | 还会返回一段摘要和便于搜索的标签 |
| 🔒 **设计上安全** | 只读；只提出标题建议，绝不修改会话 |
| ⚡ **零配置** | 单个自包含的 `SKILL.md`，无依赖 |

## 它解决的问题

自动生成的对话标题往往很笼统（比如 *"Credential information request"*），几周后很难扫读。**titlewise** 把会话的实际工作变成你会自然去搜索的标题 - 并提供十几种格式供你选择。

## 安装

### 作为插件（推荐）

```text
/plugin marketplace add Battlelamb/claude-code-conversation-titler
/plugin install titlewise@titlewise
```

之后更新：`/plugin marketplace update titlewise`。

### 作为独立技能

将技能文件夹复制到你的个人技能目录：

```text
plugins/titlewise/skills/titlewise/  ->  ~/.claude/skills/titlewise/
```

## 用法

调用它，然后回答四个简短问题：

```text
/titlewise
```

或用自然语言触发 - *"name this chat"*、*"起个标题"*、*"başlık öner"*。

**跳过提问** - 在命令中直接给出偏好：

```text
/titlewise short english slug
```

## 示例

一次完整的端到端运行。

### 1. 你调用它

```text
/titlewise
```

### 2. 它询问你想要的标题方式

一次提问，适当处支持多选：

| 问题 | 选项 |
|---|---|
| **语言** | 你的语言（自动）· 英语 · 中文 |
| **长度** | 长 · 中 · 短 |
| **日期** | 前缀 · 后缀 · 无 · 月份 |
| **风格** | 描述式 · Slug · 关键词 · 结果 · 表情 |

### 3. 它提出变体

这里以一个修复了支付超时 bug 的会话为例：

**长度 x 日期**

| 变体 | 标题 |
|---|---|
| 长 + 带日期 | `2025-03-14 - Payment API Debug (payments-service): timeout fix + retry logic + integration tests` |
| 长 | `Payment API Debug (payments-service): timeout fix + retry logic + integration tests` |
| 中 + 带日期 | `2025-03-14 - Payment API Debug (payments-service): timeout fix + retries` |
| 中 | `Payment API Debug (payments-service): timeout fix + retries` |
| 短 + 带日期 | `2025-03-14 - payment timeout fix` |
| 短 | `payment timeout fix` |

**紧凑 / 便于搜索**

| 变体 | 标题 |
|---|---|
| Slug | `payments-service-timeout-fix-2025-03-14` |
| 关键词 | `payments-service · timeout · retry · integration-tests` |
| 方括号 | `[2025-03-14][payments-service] timeout fix + retry logic` |
| 日期后缀 | `Payment API Debug (payments-service) - 2025-03-14` |
| 月份 | `2025-03 - payments-service timeout fix` |

**风格**

| 变体 | 标题 |
|---|---|
| 结果导向 | `2025-03-14 - payments-service stabilized: timeout fix + retry logic` |
| 表情 + 短 | `🐛 payments timeout fix (2025-03-14)` |

### 4. 外加描述和标签

> **描述** - 通过为 payments 服务添加带指数退避的有限重试，修复了一个请求超时 bug，并用集成测试覆盖了该路径。改动仅限于客户端层，并置于现有的超时配置开关之后。
>
> **标签** - `2025-03-14, payments-service, timeout, retry, backoff, integration-tests, bugfix`

复制你喜欢的变体，并将其设为对话标题。

## 工作原理

1. 从上下文**读取**当前对话。
2. 就*语言 / 长度 / 日期 / 风格***询问**一次 - 除非你已在命令中给出。
3. **生成**匹配的标题变体，外加描述和标签。
4. 将全部内容以可直接复制的形式**呈现**。你挑选其一并应用 - 技能绝不修改会话。

> **为什么不自动应用标题？** 对话标题由宿主应用自行管理并会自动重新生成，因此技能无法可靠地设置它，而直接编辑实时记录并不安全。**titlewise** 止步于建议 - 干净且无破坏性。

## 语言支持

标题以对话自身的语言（自动检测）、**英语**或**中文**生成 - 可同时生成一种或多种。

## 贡献

欢迎提交 issue 和 pull request。请保持技能自包含（单个 `SKILL.md`），且不含个人或环境相关内容。

## 许可证

基于 [MIT 许可证](LICENSE) 发布。
