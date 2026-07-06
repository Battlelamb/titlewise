---
name: titlewise
description: Use when the user wants to name, title, or label the current conversation, or asks for a title suggestion. Triggers on phrases like baslik oner, konusmaya isim ver, sohbeti adlandir, bu konusmaya baslik, label this chat, name this conversation, or the command /titlewise. Analyzes the current conversation, interactively asks (via AskUserQuestion) for language (user language, EN, or CHN), length, date, and style preferences unless already given, then produces the matching title variants plus a recommended pick, a short description, and tags. Suggestion only; it proposes titles you copy and apply yourself, and never modifies the session.
---

# titlewise

Generate rich, well-formatted titles (plus a description and tags) for the CURRENT conversation, so it is easy to find later by date and topic. It is interactive: it asks the user how they want the title, then produces matching variants and marks one recommended pick. Suggestion only - it proposes titles and never changes the session or its stored title.

## When to use

Trigger when the user asks to name, title, or label the current conversation - for example "baslik oner", "konusmaya isim ver", "sohbeti adlandir", "label this chat", "name this conversation", or the command `/titlewise`.

## Why suggestion-only

The host app owns the conversation title (for example, Claude Code stores and regenerates it automatically). A skill cannot reliably set it, and editing the live transcript is fragile. So this skill only PROPOSES titles: you copy the one you like and set it as the conversation title yourself, using your client's rename/title option. The skill never edits the session, the transcript, or any file.

## Workflow

Follow these steps in order when invoked.

### 1. Read the conversation
Read the current conversation from your context: main topic/project, tools, servers, people, databases, files, and what was actually done and decided. Use only what appears in the conversation - never invent details. If the conversation is empty, too short, or has no clear subject to title, say so and ask the user for a one-line hint instead of guessing.

### 2. Collect preferences (Q&A)
If the user did NOT already state preferences in their invocation, ask them in ONE `AskUserQuestion` call with these four dimensions (enable multi-select where noted):

- **Language** (multi-select): User language (the language of the conversation - auto-detect) / English (EN) / Chinese (CHN)
- **Length**: Long / Medium / Short
- **Date** (multi-select): Prefix (`YYYY-MM-DD - ...`) / Suffix (`... - YYYY-MM-DD`) / None / Month (`YYYY-MM`)
- **Style** (multi-select): Descriptive (`+` joined) / Slug (kebab-case) / Keyword (dot-separated) / Outcome-focused / Emoji

If the user already specified preferences in the invocation (e.g. `/titlewise short english slug`), skip those questions and go straight to generation. If the user gives no answer or dismisses, default to: user language + all three lengths + date prefix + descriptive.

### 3. Generate the title variant(s)
Produce the variant(s) that match the chosen dimensions, drawing from the catalog below. If multiple options were picked in a dimension, produce one variant per combination. Rules:
- Each variant is a single, copy-ready line.
- Fill the `<...>` placeholders from the conversation.
- Use today's date (from your context) as an absolute `YYYY-MM-DD`.
- Produce each variant in each selected language. Match the target language's proper characters/diacritics; when the language is Turkish, use ç, ğ, ı, ö, ş, ü.
- Never use an em dash - use a normal hyphen.

Then pick ONE **recommended** variant: the best default for scanning a history list - dated, medium length, descriptive, in the user's language, and short enough to read at a glance (aim for about 70 characters or fewer).

#### Catalog (vocabulary)

**A) Length x date**
- Long + dated: `YYYY-MM-DD - <Main Topic> (<tool/project>): <sub1> + <sub2> + ... (<people/note>)`
- Long + undated: same, without the date prefix
- Medium + dated: `YYYY-MM-DD - <Main Topic> (<tool>): <2-3 key subtopics>`
- Medium + undated: `<Main Topic> (<tool>): <2-3 key subtopics>`
- Short + dated: `YYYY-MM-DD - <3-6 word main topic>`
- Short + undated: `<3-6 word main topic>`

**B) Compact / search-friendly**
- Slug (kebab): `<tool>-<topic>-<topic>-YYYY-MM-DD` (filename-safe: only lowercase letters, digits, hyphens)
- Keyword (dot): `<tool> · <topic1> · <topic2> · <topic3>`
- Bracket tag: `[YYYY-MM-DD][<tool>] <topic1> + <topic2>`
- Date suffix: `<Main Topic> (<tool>) - YYYY-MM-DD`
- Month: `YYYY-MM - <tool> <main topic>`

**C) Style**
- Outcome-focused: `YYYY-MM-DD - <tool> <outcome>: <main-work1> + <main-work2>`
- Emoji + short: `<emoji> <tool> <main topic> (YYYY-MM-DD)` - pick the emoji from the dominant work type:
  feature ✨ · new/launch 🎉 · bugfix 🐛 · fix/patch 🔧 · refactor ♻️ · docs 📝 · perf ⚡ · security 🔒 ·
  release/ship 🚀 · config ⚙️ · tests ✅ · data/db 🗄️ · infra 🏗️ · design/ui 🎨 · research 🔎

For more options, cross-product the dimensions: language x length x date-position x style.

### 4. Description
Write a 3-6 sentence summary paragraph (what was done, the outcome), in the selected language.

### 5. Tags
Give 5-8 comma-separated lowercase kebab tags: date + entities (tool, server/IP, people, database) + topics.

### 6. Present the results
Lead with the **recommended** title in a fenced code block (so it is one-click copy-ready). Then show the full title variants as a clearly labeled, copy-ready list grouped by category, followed by the description and the tags. End with a one-line note: copy the variant you like and set it as the conversation title using your client's rename/title option. Do not run or emit any command to apply the title, and do not edit any file.

## Generic example (illustrative only)

For a session that fixed a payment timeout bug:
- Recommended: `2025-03-14 - Payment API Debug (payments-service): timeout fix + retries`
- Long + dated: `2025-03-14 - Payment API Debug (payments-service): timeout fix + retry logic + integration tests`
- Short + dated: `2025-03-14 - payment timeout fix`
- Slug: `payments-service-timeout-fix-2025-03-14`
- Keyword: `payments-service · timeout · retry · integration-tests`
- Emoji: `🐛 payments timeout fix (2025-03-14)`
- Tags: `2025-03-14, payments-service, timeout, retry, backoff, integration-tests, bugfix`

## Rules

- Never use an em dash; use a normal hyphen.
- Match the output language's proper characters; when Turkish, use ç, ğ, ı, ö, ş, ü.
- Each title variant is one line, copy-ready, with no trailing punctuation.
- The slug variant is filename-safe: only lowercase letters, digits, and hyphens.
- Never invent details - use only what the conversation contains; if there is nothing to title, ask for a hint.
- Suggestion only: never edit the transcript or the app's title store, and never emit a command to apply the title.
