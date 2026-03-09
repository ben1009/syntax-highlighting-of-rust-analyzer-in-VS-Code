# VSCode to Zed Migration Guide

This document describes how to migrate from VSCode to Zed using the converted settings.

## Quick Start

1. Copy `.zed/settings.json` to your Zed configuration directory:
   - **Linux**: `~/.config/zed/settings.json`
   - **macOS**: `~/Library/Application Support/Zed/settings.json`

2. Install [Fira Code](https://github.com/tonsky/FiraCode) font if you haven't already

3. Restart Zed or press `Cmd+Shift+P` (macOS) / `Ctrl+Shift+P` (Linux) and type "zed: reload settings"

## Settings Comparison

| VSCode Setting | Zed Equivalent | Status |
|---------------|----------------|--------|
| `editor.fontSize: 11` | `buffer_font_size: 11` | ✅ |
| `editor.fontFamily: "Fira Code"` | `buffer_font_family: "Fira Code"` | ✅ |
| `editor.fontLigatures: true` | `buffer_font_features` | ✅ |
| `workbench.sideBar.location: "right"` | `project_panel.dock: "right"` | ✅ |
| `files.autoSave: "afterDelay"` | `auto_save.after_delay` | ✅ |
| `editor.formatOnSave: true` | `format_on_save: "on"` | ✅ |
| `editor.wordWrap: "on"` | `soft_wrap: "editor_width"` | ✅ |
| `rust-analyzer.check.command: "clippy"` | `lsp.rust-analyzer.initialization_options` | ✅ |
| `editorInlayHint.*` | `inlay_hints.*` | ✅ |

## Known Differences

### Theme Colors
Zed doesn't support the same level of semantic token color customization as VSCode. The `editor.semanticTokenColorCustomizations` and `editor.tokenColorCustomizations` from VSCode cannot be directly ported.

**Workarounds:**
- Install a Zed theme extension that matches your preference
- Use Zed's experimental custom CSS feature
- Use the built-in theme overrides in Zed settings

### Extensions

| VSCode Extension | Zed Alternative |
|-----------------|-----------------|
| GitLens | Built-in Git support (`git.inline_blame`) |
| ErrorLens | Built-in diagnostics inline |
| TODO Highlight | Use Zed's search or install extension |
| rust-test-lens | Built-in test runner |
| Codeium | Built-in Assistant or Codeium extension |

## Language Support

### Rust
- rust-analyzer is automatically detected and configured
- Clippy is enabled by default (as per your VSCode settings)
- Inlay hints are enabled

### Go
- Ensure `gopls` is installed: `go install golang.org/x/tools/gopls@latest`
- Format on save is enabled

## Tips

1. **Command Palette**: `Cmd+Shift+P` (macOS) / `Ctrl+Shift+P` (Linux)
2. **File Finder**: `Cmd+P` / `Ctrl+P`
3. **Project Search**: `Cmd+Shift+F` / `Ctrl+Shift+F`
4. **Vim Mode**: Add `"vim_mode": true` to settings if needed

## Troubleshooting

### Font not showing correctly
Make sure Fira Code is installed on your system:
```bash
# macOS
brew install font-fira-code

# Arch Linux
sudo pacman -S ttf-fira-code

# Ubuntu/Debian
cd /tmp
wget https://github.com/tonsky/FiraCode/releases/download/6.2/Fira_Code_v6.2.zip
unzip Fira_Code_v6.2.zip -d ~/.local/share/fonts/
fc-cache -f
```

### rust-analyzer not working
Ensure it's in your PATH:
```bash
which rust-analyzer
# or
rustup component add rust-analyzer
```

## References

- [Zed Documentation](https://zed.dev/docs/)
- [Zed Settings Reference](https://zed.dev/docs/configuring-zed)
- Original VSCode settings: [setting.json](./setting.json)
