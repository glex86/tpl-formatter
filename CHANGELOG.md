# Change Log

All notable changes to the "Smarty Formatter" extension will be documented in this file.

## [2.1.2] - 2025-12-29

### Added

- Enhanced formatting algorithm with improved tag wrapping logic
- Support for `{component}` tags with dedicated snippet
- Support for `{include_scoped}` tags with dedicated snippet
- Support for `{sectionelse}` middle tag in formatting
- Improved handling of multiline tag formatting
- Enhanced logic tag detection (if, elseif, while)
- Better indentation preservation for complex nested structures

### Changed

- Completely rewritten beautify.ts with advanced preprocessing and postprocessing
- Improved syntax highlighting with better structure and readability
- Enhanced language configuration with proper formatting
- Updated logo with higher resolution (69KB)
- Code refactoring for better maintainability

### Fixed

- Fixed indentation issues in nested Smarty tags
- Improved handling of HTML tags within Smarty templates
- Better preservation of whitespace in formatted code
- Fixed wrapping behavior for long tags

## Previous Versions

See git history for earlier changes.
