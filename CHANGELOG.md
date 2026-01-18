# Changelog

All notable changes to the **TPL Formatter** extension are documented in this file.

This project is a **new, independent extension** with its own versioning history.

---

## [0.2.1] – 2026-01-18

### Fixed

- **Critical Literal Handling Fix**:
  - Implemented an advanced **Context-Aware Strategy** for `{literal}` blocks.
  - HTML attributes using `{literal}` (e.g., `data-val="{literal}...{/literal}"`) are now protected from being mangled or collapsed by the formatter.
  - `<script>` content inside `{literal}` blocks is now correctly identified and formatted as JavaScript.
  - Corrected indentation issues where `{literal}` blocks inside attributes would lose alignment or create excessive gaps.
  - Fixed a bug where nested braces `{}` inside literal blocks (e.g., in JSON objects) broke the parser.

### Added

- **Smarty Array Formatting**:
  - Added support for auto-formatting Smarty arrays within tags (e.g., `values=['a', 'b', 'c']`).
  - Arrays are now split across multiple lines for better readability when inside long tags.

- **Attribute Indentation Improvements**:
  - Optimized indentation logic for multiline attributes to ensure consistent alignment with the parent tag.

---

## [0.1.0] – 2025-12-29

### Initial Release

This is the first public release of **TPL Formatter** as a standalone and community-maintained extension.

### Added

- Core Smarty-aware formatting engine with tag wrapping logic
- Support for `{component}` and `{include_scoped}` snippets
- Support for `{sectionelse}` middle tag handling
- Multiline Smarty tag formatting support
- Improved detection of logic tags (`if`, `elseif`, `while`)
- Indentation preservation for nested Smarty structures

### Changed

- Initial implementation of the formatting pipeline (`beautify.ts`)
- Language configuration tuned for formatting stability
- Custom branding and extension icon

### Fixed

- Indentation issues in nested Smarty blocks
- Formatting inconsistencies in mixed HTML and Smarty templates

---

## Previous history

No previous versions exist prior to `0.1.0`.
Earlier experimentation and refactoring can be found in the Git commit history.
