# Changelog

All notable changes to **titlewise** are documented here. The format follows
[Keep a Changelog](https://keepachangelog.com/) and [Semantic Versioning](https://semver.org/).

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
