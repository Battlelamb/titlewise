<div align="center">

<img src="assets/banner.png" alt="titlewise - title, name and label your Claude Code conversations" width="100%">

**A [Claude Code](https://code.claude.com) skill that turns any conversation into a title you can actually find later.**

[![Release](https://img.shields.io/github/v/release/Battlelamb/claude-code-conversation-titler?style=flat-square&color=2dcd7a&logo=github&label=release)](https://github.com/Battlelamb/claude-code-conversation-titler/releases)
&nbsp;[![Stars](https://img.shields.io/github/stars/Battlelamb/claude-code-conversation-titler?style=flat-square&color=8b5cf6&logo=github)](https://github.com/Battlelamb/claude-code-conversation-titler/stargazers)
&nbsp;[![License](https://img.shields.io/badge/license-MIT-22d3ee?style=flat-square)](LICENSE)
&nbsp;[![Claude Code](https://img.shields.io/badge/Claude_Code-skill_%26_plugin-ec4899?style=flat-square)](https://code.claude.com)
&nbsp;[![PRs welcome](https://img.shields.io/badge/PRs-welcome-2dcd7a?style=flat-square)](#contributing)

<br>

<img src="assets/demo.gif" alt="titlewise demo - interactive conversation title generation" width="760">

</div>

---

## Overview

**titlewise** is an interactive Claude Code skill that reads your current conversation and proposes clean, well-structured **titles** - long or short, dated or not, in your own language, English, or Chinese - along with a short description and search tags. You pick the one you like and set it as the conversation title.

Think of it as a **conversation title generator** for Claude Code: name, title, or label any chat session in seconds, so past conversations are easy to find later.

It is **suggestion-only**: it proposes, you apply. It never touches your session or transcript.

## Features

| | |
|---|---|
| 🎛️ **Interactive** | Asks how you want the title (language, length, date, style) before generating |
| 🌍 **Multilingual** | Your conversation's language (auto-detected), English, or Chinese - pick one or several |
| 📏 **13+ variants** | Long / medium / short, dated / undated, slug, keyword, bracket, month, outcome, emoji |
| 📝 **More than a title** | Also returns a one-paragraph recap and search-friendly tags |
| 🔒 **Safe by design** | Read-only; it proposes titles and never edits the session |
| ⚡ **Zero config** | A single self-contained `SKILL.md`, no dependencies |

## The problem it solves

Auto-generated conversation titles are generic (think *"Credential information request"*) and hard to scan weeks later. **titlewise** turns the actual work of the session into a title you would naturally search for - and gives you a dozen formats to choose from.

## Installation

### As a plugin (recommended)

```text
/plugin marketplace add Battlelamb/claude-code-conversation-titler
/plugin install titlewise@titlewise
```

Update later with `/plugin marketplace update titlewise`.

### As a standalone skill

Copy the skill folder into your personal skills directory:

```text
plugins/titlewise/skills/titlewise/  ->  ~/.claude/skills/titlewise/
```

## Usage

Invoke it, then answer the four quick questions:

```text
/titlewise
```

Or trigger it in natural language - *"name this chat"*, *"suggest a title"*, *"başlık öner"*.

**Skip the questions** by passing your preferences inline:

```text
/titlewise short english slug
```

## Example

A full run, end to end.

### 1. You invoke it

```text
/titlewise
```

### 2. It asks how you want the title

One prompt, multi-select where it makes sense:

| Question | Options |
|---|---|
| **Language** | Your language (auto) · English · Chinese |
| **Length** | Long · Medium · Short |
| **Date** | Prefix · Suffix · None · Month |
| **Style** | Descriptive · Slug · Keyword · Outcome · Emoji |

### 3. It proposes variants

Here, for a session that fixed a payment timeout bug:

**Length x date**

| Variant | Title |
|---|---|
| Long + dated | `2025-03-14 - Payment API Debug (payments-service): timeout fix + retry logic + integration tests` |
| Long | `Payment API Debug (payments-service): timeout fix + retry logic + integration tests` |
| Medium + dated | `2025-03-14 - Payment API Debug (payments-service): timeout fix + retries` |
| Medium | `Payment API Debug (payments-service): timeout fix + retries` |
| Short + dated | `2025-03-14 - payment timeout fix` |
| Short | `payment timeout fix` |

**Compact / search-friendly**

| Variant | Title |
|---|---|
| Slug | `payments-service-timeout-fix-2025-03-14` |
| Keyword | `payments-service · timeout · retry · integration-tests` |
| Bracket | `[2025-03-14][payments-service] timeout fix + retry logic` |
| Date suffix | `Payment API Debug (payments-service) - 2025-03-14` |
| Month | `2025-03 - payments-service timeout fix` |

**Style**

| Variant | Title |
|---|---|
| Outcome-focused | `2025-03-14 - payments-service stabilized: timeout fix + retry logic` |
| Emoji + short | `🐛 payments timeout fix (2025-03-14)` |

### 4. Plus a description and tags

> **Description** - Fixed a request-timeout bug in the payments service by adding bounded retries with exponential backoff, then covered the path with integration tests. The change is isolated to the client layer and ships behind the existing timeout config.
>
> **Tags** - `2025-03-14, payments-service, timeout, retry, backoff, integration-tests, bugfix`

Copy the variant you like and set it as the conversation title.

## How it works

1. **Reads** the current conversation from context.
2. **Asks** once for *language / length / date / style* - unless you passed them inline.
3. **Generates** the matching title variants, plus a description and tags.
4. **Presents** everything copy-ready. You choose one and apply it in your client - the skill never edits the session.

> **Why not apply the title automatically?** The host app owns the conversation title and regenerates it on its own, so a skill cannot reliably set it and editing the live transcript is unsafe. **titlewise** stops at proposing - clean and non-destructive.

## Language support

Titles are produced in your **conversation's own language** (auto-detected), **English**, or **Chinese** - one or several at once.

## Contributing

Issues and pull requests are welcome. Please keep the skill self-contained (a single `SKILL.md`) and free of personal or environment-specific content.

## License

Released under the [MIT License](LICENSE).
