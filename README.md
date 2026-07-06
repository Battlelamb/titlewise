<div align="center">

# 🏷️ conversation-labeler

**Turn any Claude Code conversation into a title you can actually find later.**

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
&nbsp;![Claude Code](https://img.shields.io/badge/Claude%20Code-skill%20%26%20plugin-8A2BE2)
&nbsp;![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)

</div>

---

## Overview

**conversation-labeler** is an interactive [Claude Code](https://code.claude.com) skill that reads your current conversation and proposes clean, well-structured **titles** - long or short, dated or not, in your own language, English, or Chinese - along with a short description and search tags. You pick the one you like and set it as the conversation title.

It is **suggestion-only**: it proposes, you apply. It never touches your session or transcript.

## Features

| | |
|---|---|
| 🎛️ **Interactive** | Asks how you want the title (language, length, date, style) before generating |
| 🌍 **Multilingual** | Your conversation's language (auto-detected), English, or Chinese - pick one or several |
| 📏 **Many variants** | Long / medium / short, dated / undated, slug, keyword, bracket, emoji, and more |
| 📝 **More than a title** | Also returns a one-paragraph recap and search-friendly tags |
| 🔒 **Safe by design** | Read-only; it proposes titles and never edits the session |
| ⚡ **Zero config** | A single self-contained `SKILL.md`, no dependencies |

## The problem it solves

Auto-generated conversation titles are generic (think *"Credential information request"*) and hard to scan weeks later. conversation-labeler turns the actual work of the session into a title you would naturally search for - and gives you several formats to choose from.

## Installation

### As a plugin (recommended)

```
/plugin marketplace add Battlelamb/conversation-labeler
/plugin install conversation-labeler@conversation-labeler
```

Update later with `/plugin marketplace update conversation-labeler`.

### As a standalone skill

Copy the skill folder into your personal skills directory:

```
plugins/conversation-labeler/skills/conversation-labeler/  ->  ~/.claude/skills/conversation-labeler/
```

## Usage

Invoke it, then answer the four quick questions:

```
/conversation-labeler
```

Or trigger it in natural language - *"name this chat"*, *"suggest a title"*, *"başlık öner"*.

**Skip the questions** by passing your preferences inline:

```
/conversation-labeler short english slug
```

## Example

For a session that fixed a payment timeout bug, you might get:

**Long + dated**
`2025-03-14 - Payment API Debug (payments-service): timeout fix + retry logic + integration tests`

**Short + dated**
`2025-03-14 - payment timeout fix`

**Slug**
`payments-service-timeout-fix-2025-03-14`

**Keyword**
`payments-service · timeout · retry · integration-tests`

**Description**
> Fixed a request-timeout bug in the payments service by adding bounded retries with backoff, then covered the path with integration tests. The change is isolated to the client layer and ships behind the existing timeout config.

**Tags**
`2025-03-14, payments-service, timeout, retry, integration-tests`

Copy the variant you like and set it as the conversation title.

## How it works

1. **Reads** the current conversation from context.
2. **Asks** once for *language / length / date / style* - unless you passed them inline.
3. **Generates** the matching title variants, plus a description and tags.
4. **Presents** everything copy-ready. You choose one and apply it in your client - the skill never edits the session.

> **Why not apply the title automatically?** The host app owns the conversation title and regenerates it on its own, so a skill cannot reliably set it and editing the live transcript is unsafe. conversation-labeler stops at proposing - clean and non-destructive.

## Language support

Titles are produced in your **conversation's own language** (auto-detected), **English**, or **Chinese** - one or several at once.

## Contributing

Issues and pull requests are welcome. Please keep the skill self-contained (a single `SKILL.md`) and free of personal or environment-specific content.

## License

Released under the [MIT License](LICENSE).
