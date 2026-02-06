# TPL Formatter AI Agent Instructions

## Project Overview
VS Code extension for formatting Smarty (`.tpl`) templates using Language Server Protocol (LSP). Handles mixed Smarty + HTML/CSS/JS with context-aware parsing.

## Architecture

### Client-Server LSP Model
- **Client** (`client/src/`): VS Code extension host, registers providers
- **Server** (`server/src/`): Separate Node.js process, handles formatting/folding/diagnostics
- Communication via IPC using `vscode-languageclient` and `vscode-languageserver`
- Dual bundles: Node (`dist/node/`) for desktop, `dist/browser/` for web

### Key Files
- `client/src/extension.ts` - Extension entry, registers providers & commands
- `client/src/language/beautify.ts` - **Core formatter** (BeautifySmarty class)
- `client/src/language/formatter.ts` - DocumentFormattingEditProvider implementation
- `server/src/htmlServer.ts` - Language server entry point
- `server/src/modes/formatting.ts` - Orchestrates HTML/JS/CSS formatting

## Formatting Pipeline (BeautifySmarty)

The formatter uses a 5-phase pipeline in `client/src/language/beautify.ts`:

```
Phase 1: PREPROCESS
  - Extract Smarty tags (e.g., {if $var}, {foreach})
  - Replace with pseudo-HTML tags (<vsc-smarty-if>, <vsc-smarty-foreach>)
  - Handle {literal} blocks with context-aware strategy (see below)

Phase 2: BEAUTIFY
  - Run js-beautify on pseudo-HTML
  - Respects editor.tabSize, editor.insertSpaces

Phase 3: POSTPROCESS
  - Restore pseudo-HTML back to Smarty tags
  - Restore {literal} blocks with proper indentation

Phase 4: INDENT PASS
  - Line-by-line: Track indent stack for nested {if}, {foreach}, {for}, {while}
  - De-indent middle tags: {else}, {elseif}, {foreachelse}

Phase 5: WRAP LONG TAGS
  - Split multiline {component}, {include} attributes across lines
```

## Critical Pattern: {literal} Context-Aware Handling

Smarty's `{literal}` disables brace parsing. The formatter uses **3-tier context detection**:

1. **In `<script>` or `<style>`**: Wrap in JS comments `/*___VSC_LIT_START___*/.../*___VSC_LIT_END___*/`
2. **In HTML attributes** (e.g., `<div data="{literal}...{/literal}">`): Use opaque tokens `___VSC_SMARTY_LITERAL_BLOCK_N___`
3. **In HTML content**: Wrap in HTML comments `<!--___VSC_LIT_START___-->...<!--___VSC_LIT_END___-->`

**Why**: Prevents js-beautify from mangling literal content while allowing surrounding code to format correctly.

## Build & Test Commands

```bash
# Install dependencies (runs postinstall hook)
npm install

# Development build (watch mode)
npm run watch         # Desktop bundle
npm run watch-web     # Browser bundle

# Production build
npm run package       # Desktop (hidden source maps)
npm run package-web   # Browser (hidden source maps)

# Test
npm test              # Runs sh ./scripts/e2e.sh (if exists)
cd server && npm test # Unit tests (server/src/test/*.test.ts)
```

## Testing Patterns

From `server/src/test/formatting.test.ts`:

- Use `suite()` for grouping related tests
- Helper: `assertFormat(input, expected, options)` - formats and compares
- Range marking: Pipe `|` characters denote format ranges (`'|<html>|'` = full doc)
- Fixtures: Separate input/output files in `test/fixtures/`

Example:
```typescript
test('Format Smarty if block', async () => {
  await assertFormat('|{if $var}<div></div>{/if}|', 
    '{if $var}\n\t<div></div>\n{/if}');
});
```

## Coding Conventions

- **Classes**: PascalCase (`BeautifySmarty`, `FormattingProvider`)
- **Functions**: camelCase with action verbs (`preprocess()`, `beautify()`)
- **Constants**: UPPER_SNAKE_CASE or PascalCase objects
- **Error handling**: Wrapped in `runSafe()` with LSP `ResponseError` types
- **Configuration**: Singleton `CONFIG` object in `configuration.ts`, updated via `setConfiguration()`

## Important Patterns

### Working with LSP Ranges/Positions
```typescript
const range = Range.create(document.positionAt(start), document.positionAt(end));
const edit = TextEdit.replace(range, newText);
```

### State Management in BeautifySmarty
- `private smartyTags: string[]` - Stores extracted tags during pipeline
- `private literals: FormattingLiterals` - Regex patterns for literal detection
- Pipeline phases modify and restore state sequentially

## Common Tasks

**Adding new Smarty tag support**: Update `tags` Sets in `beautify.ts` (startTags, middleTags, endTags)

**Changing indentation logic**: Modify Phase 4 in `beautify.ts` (indent stack tracking)

**Fixing literal handling**: Update context detection in `preprocess()` method

**Adding tests**: Create new `.test.ts` in `server/src/test/` using `assertFormat()` pattern
