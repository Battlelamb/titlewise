# Changelog

All notable changes to **titlewise** are documented here. The format follows
[Keep a Changelog](https://keepachangelog.com/) and [Semantic Versioning](https://semver.org/).

## [1.1.2] - 2026-07-09

### Fixed
- **The Style question could not be asked.** `AskUserQuestion` accepts at most 4 options per question, and Style had grown to 6 (Descriptive, Slug, Keyword, Bracket, Outcome-focused, Emoji), so the tool call was rejected. Style is now 4 options - `Descriptive`, `Compact`, `Outcome-focused`, `Emoji` - where **Compact** expands into the slug, keyword, and bracket variants. All six catalogued styles remain reachable. (Introduced in 1.1.1 by making Bracket selectable.)
- **Length is now multi-select**, matching the documented default of "all three lengths". Previously the default promised three lengths but the question only allowed one.

### Added
- **A 12-variant cap per language.** With four multi-select dimensions the full cross-product could reach dozens of lines; the skill now keeps the recommended pick plus the most distinct variants and reports how many combinations were suppressed.
- Explicit rules recording the `AskUserQuestion` limits (max 4 questions, max 4 options each), so a future style is added by expanding an option rather than adding a fifth.

### Changed
- The three READMEs now show the corrected Style row; the English one had also drifted, still listing the pre-1.1.1 set without Bracket.

## [1.1.1] - 2026-07-06

### Fixed
- **Bracket** is now a selectable Style option, so every catalogued variant is reachable from the Q&A.
- The **recommended pick** no longer overrides the user's own dimension choices - it chooses the best among the variants actually produced.
- Clarified the Keyword separator (middot `·`) and how the Date dimension interacts with date-carrying styles (slug, month, bracket).

### Changed
- Example description extended to satisfy the 3-6 sentence rule; the PRs-welcome badge now points to the pull-requests page across all READMEs.
- Added a `keywords` array to the plugin manifest for discoverability.

## [1.1.0] - 2026-07-06

### Added
- **Recommended pick** - one variant is highlighted as the best default and shown copy-ready.
- **Outcome emoji map** - the emoji variant matches the session's dominant work type (bugfix, feature, refactor, release, ...).
- **Animated demo** in the README.
- Graceful handling when the conversation has no clear subject to title (asks for a hint instead of guessing).

### Changed
- Slug variant is now filename-safe (lowercase letters, digits, and hyphens only).
- Tags capped at 5-8; description kept to 3-6 sentences; titles carry no trailing punctuation.

## [1.0.0] - 2026-07-06

### Added
- Initial release - interactive, multilingual (user language / EN / CHN) conversation titler.
- 13+ title formats, a short description, and search tags.
- Install as a Claude Code plugin (marketplace) or as a standalone skill.
