# Smarty Formatter

![Smarty Logo](images/logo.png)

Smarty Formatter for Visual Studio Code with formatting, folding, snippets, syntax highlighting and more.

## Features

### 🎨 Syntax Highlighting

- Full syntax highlighting for Smarty template files (.tpl)
- Support for embedded HTML, CSS, and JavaScript
- Proper color coding for Smarty tags, variables, and functions

### ✨ Code Formatting

- Advanced formatting engine based on js-beautify
- Smart indentation for nested Smarty tags
- Proper handling of:
  - Block tags (if, foreach, for, while, function, etc.)
  - Middle tags (else, elseif, foreachelse, sectionelse)
  - Component and include tags
  - HTML and embedded scripts

### 📝 Snippets

Built-in snippets for common Smarty constructs:

- `block` - Block tag
- `capture` - Capture tag
- `component` - Component include tag (**New in 2.1.2**)
- `for` - For loop
- `foreach` - Foreach loop
- `function` - Function definition
- `if` / `elseif` / `else` - Conditional statements
- `include` - Include template
- `include_scoped` - Scoped include template (**New in 2.1.2**)
- `literal` - Literal block
- `section` - Section loop
- And many more...

### 🔧 Additional Features

- Code folding for Smarty blocks
- Auto-closing pairs for braces and brackets
- Comment toggling with `{* *}`
- Highlight decoration toggle (optional)

## Installation

1. Open Visual Studio Code
2. Press `Ctrl+P` / `Cmd+P` to open Quick Open
3. Type `ext install OktayAydoan.smarty-formatter`
4. Press Enter

## Usage

### Formatting

- **Format Document**: `Shift+Alt+F` (Windows/Linux) or `Shift+Option+F` (macOS)
- **Format Selection**: Select code and use the same shortcut

The formatter respects your VS Code settings:

- `editor.tabSize` - Number of spaces for indentation
- `editor.insertSpaces` - Use spaces or tabs

### Highlight Decoration

Toggle highlight decoration for Smarty tags:

- Open Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
- Type "Smarty: Toggle Highlight Decoration"

## Configuration

```json
{
	// Enable/disable highlight decoration
	"smarty.highlight": false,

	// Customize highlight colors
	"smarty.highlightColor": {
		"dark": "#FFFFFF25",
		"light": "#FFFA0040"
	}
}
```

## Supported Smarty Tags

### Block Tags

- `{block}`, `{capture}`, `{for}`, `{foreach}`, `{function}`
- `{if}`, `{literal}`, `{section}`, `{setfilter}`, `{strip}`, `{while}`

### Inline Tags

- `{assign}`, `{component}`, `{include}`, `{include_scoped}`
- `{append}`, `{break}`, `{call}`, `{continue}`
- `{debug}`, `{extends}`, `{insert}`, `{ldelim}`, `{rdelim}`

### Built-in Functions

- Variables: `{$variable}`, `{$array.key}`, `{$object->property}`
- Modifiers: `{$var|modifier:param}`
- Functions: `{counter}`, `{cycle}`, `{eval}`, `{fetch}`, `{html_*}`, `{mailto}`, etc.

## What's New in 2.1.2

- ✅ Enhanced formatting algorithm with better tag wrapping
- ✅ New snippets: `{component}` and `{include_scoped}`
- ✅ Support for `{sectionelse}` middle tag
- ✅ Improved multiline tag handling
- ✅ Better indentation for nested structures
- ✅ Updated logo with higher resolution
- ✅ Code refactoring for improved performance

## Requirements

- Visual Studio Code v1.43.0 or higher

## Known Issues

- Some complex nested structures may require manual adjustment
- Performance may vary with very large template files

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Repository

https://github.com/oktayaydogan/smarty-formatter

## License

MIT License - see LICENSE file for details

## Author

Oktay Aydoğan

- Email: aydoganooktay@gmail.com

---

**Enjoy coding with Smarty! 🚀**
