# HELIX EDITOR
1. config.toml
```
theme = "catppuccin_mocha"

[editor]
bufferline = "multiple"
# bufferline = "never"
# cursorline = true
line-number = "relative"
rulers = [120]
true-color = true
mouse = true
scrolloff = 10
shell = ["zsh", "-c"]
color-modes = true
gutters = ["diagnostics", "spacer", "line-numbers", "spacer", "diff"]
auto-pairs = true
idle-timeout = 50

[editor.cursor-shape]
insert = "bar"
normal = "block"
select = "underline"

[editor.indent-guides]
character = "╎"
render = true
skip-levels = 1


[editor.file-picker]
hidden = false
parents = false
git-ignore = false

# [editor.whitespace]
# render = "all"

[editor.statusline]
left = [
  "mode",
  "spacer",
  "version-control",
  "spacer",
  "separator",
  "file-name",
  "file-modification-indicator"
]
right = [
  "spinner",
  "spacer",
  "workspace-diagnostics",
  "separator",
  "spacer",
  "diagnostics",
  "position",
  "file-encoding",
  "file-line-ending",
  "file-type"
]
separator = "╎"
mode.normal = "NORMAL"
mode.insert = "INSERT"
mode.select = "SELECT"


[editor.lsp]
# auto-signature-help = true
# display-signature-help-docs = true
display-messages = true
display-inlay-hints = true

[keys.normal]
C-s = ":w"
G = "goto_file_end"

V = ["select_mode", "extend_to_line_bounds"]
d = { d = ["extend_to_line_bounds", "delete_selection"], t = ["extend_till_char"], s = ["surround_delete"], i = ["select_textobject_inner"], a = ["select_textobject_around"] }
# Clipboards over registers ye ye
x = "delete_selection"
p = "paste_clipboard_after"
P = "paste_clipboard_before"
# Would be nice to add ya and yi, but the surround commands can't be chained
y = ["yank_main_selection_to_clipboard", "normal_mode", "flip_selections", "collapse_selection"]
# y = "yank_joined_to_clipboard" # use my system clipboard

Y = ["extend_to_line_bounds", "yank_main_selection_to_clipboard", "goto_line_start", "collapse_selection"]
o = ["open_below", "normal_mode"]
O = ["open_above", "normal_mode"]
# Uncanny valley stuff, this makes w and b behave as they do Vim
w = ["move_next_word_start", "move_char_right", "collapse_selection"]
e = ["move_next_word_end", "collapse_selection"]
b = ["move_prev_word_start", "collapse_selection"]
"tab" = ":bn"
"S-tab" = ":bp"
esc = ["collapse_selection", "keep_primary_selection"]

[keys.normal.space]
q = ":q"
Q = ":qa!"
x = ":buffer-close"
X = ":buffer-close-others"
n = ":new"

[keys.normal.space.c]
r = [":w", ":config-reload"]
o = ":config-open"
l = ":o ~/.config/helix/languages.toml" 
  
[keys.insert]
j = { k = "normal_mode" } # Maps `jk` to exit insert mode
k = { j = "normal_mode" }
esc = ["collapse_selection", "normal_mode"]

[keys.select]
esc = ["collapse_selection", "keep_primary_selection", "normal_mode"]
G = "goto_file_end"
# x = "delete_selection"
x = ["yank_main_selection_to_clipboard", "delete_selection"]
y = ["yank_main_selection_to_clipboard", "normal_mode", "flip_selections", "collapse_selection"]
Y = ["extend_to_line_bounds", "yank_main_selection_to_clipboard", "goto_line_start", "collapse_selection", "normal_mode"]
d = ["yank_main_selection_to_clipboard", "delete_selection"]
p = "replace_selections_with_clipboard" # No life without this
P = "paste_clipboard_before"
```
2. languages.toml
1. 
```
[[language]]
name = "rust"
scope = "source.rust"
injection-regex = "(rust|rs)"
file-types = ["rs"]
roots = ["Cargo.toml", "Cargo.lock"]
auto-format = true
comment-token = "//"
language-servers = [ "rust-analyzer" ]
indent = { tab-width = 4, unit = "    " }


[language.debugger]
name = "lldb-vscode"
transport = "stdio"
command = "lldb-vscode"

[[language.debugger.templates]]
name = "binary"
request = "launch"
completion = [ { name = "binary", completion = "filename" } ]
args = { program = "{0}", initCommands = [ "command script import /usr/local/etc/lldb_vscode_rustc_primer.py" ] }

[language-server.rust-analyzer]
command = "rust-analyzer"

[language-server.rust-analyzer.config]
inlayHints.bindingModeHints.enable = false
inlayHints.closingBraceHints.minLines = 10
inlayHints.closureReturnTypeHints.enable = "with_block"
inlayHints.discriminantHints.enable = "fieldless"
inlayHints.lifetimeElisionHints.enable = "skip_trivial"
inlayHints.typeHints.hideClosureInitialization = false

[language-server.rust-analyzer.config.check]
command = "clippy"

[language.auto-pairs]
'(' = ')'
'{' = '}'
'[' = ']'
'"' = '"'
'`' = '`'

[[grammar]]
name = "rust"
source = { git = "https://github.com/tree-sitter/tree-sitter-rust", rev = "0431a2c60828731f27491ee9fdefe25e250ce9c9" }

```
3. Docs


