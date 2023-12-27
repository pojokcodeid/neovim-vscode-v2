# PANDUAN CONFIG NEOVIM, VASCODE DAN VSPACECODE

### Pastikan sudah install Neovim

### Pastikan sudah install Visual Studio Code

### List Extenstion

- https://marketplace.visualstudio.com/items?itemName=asvetliakov.vscode-neovim
- https://marketplace.visualstudio.com/items?itemName=JulianIaquinandi.nvim-ui-modifier
- https://marketplace.visualstudio.com/items?itemName=VSpaceCode.vspacecode
- https://marketplace.visualstudio.com/items?itemName=PojokCode.pcode-icon
- https://marketplace.visualstudio.com/items?itemName=PojokCode.pcode-theme

### Buat Configurasi Neovim dengan struktur Sebagai Berikut

```bash

├── init.lua
├── lua
│   └── vscode
│       ├── functions.lua
│       └── mappings.lua
└── README.md

```

nvim/init.lua

```lua
if vim.g.vscode then
  -- config vscode
  Map = vim.keymap.set
  Cmd = vim.cmd
  VSCodeNotify = vim.fn.VSCodeNotify
  VSCodeCall = vim.fn.VSCodeCall

  require("vscode.functions")
  require("vscode.mappings")
else
  -- config neovim disini
end
```

nvim/lua/vscode/functions.lua

```lua
function Active_whichkey()
	VSCodeNotify("vspacecode.space")
end

---- dst ... lengkapnya cek file functions.lua

```

nvim/lua/vscode/mappings.lua

```lua
-- n = normal mode
-- i = insert mode
-- v = visual mode
-- x = visual block mode
-- t = terminal mode
-- c = command mode
-- o = operator pending mode

-- Map("", "L", Move_to_bottom_screen)
-- Map("", "H", Move_to_top_screen)
-- Map("", "<Space>", Trim__save__no_highlight)
Map({ "n", "x" }, "<Space>", Active_whichkey)
-- Map({ "n", "x" }, "<C-j>", Navigation_down)
-- Map({ "n", "x" }, "<C-k>", Navigation_up)
-- Map({ "n", "x" }, "<C-h>", Navigation_left)
-- Map({ "n", "x" }, "<C-l>", Navigation_right)
Map("", "U", Trim__save__format)

Map("n", "gD", Reveal_definition_aside)
Map("n", "gt", Go_to_implementation)
Map("n", "gq", Go_to_reference)
Map("n", ",r", Rename_symbol)
Map("n", "<<", Outdent)
Map("n", ">>", Indent)
Map("n", "gcc", Comment)
Map("n", "=s", Convert_to_spaces)
Map("n", "=t", Convert_to_tabs)
Map("n", "=d", Indent_with_spaces)
Map("n", "=g", Indent_with_tabs)
Map("n", "K", CloseEditor)
Map("n", ",K", UndoCloseEditor)
Map("n", "zk", Git_stage_file)
Map("n", "zK", Git_unstage_file)
Map("n", "zi", Git_open_changes)
Map("n", "zI", Git_open_all_changes)
Map("n", "zy", Toggle_breakpoint)
Map("n", "yr", Copy_relative_path)
Map("n", "yR", Copy_path)
Map({ "n", "i", "v", "x" }, "<C-a>", Select_all)
Map({ "n", "v", "x" }, "y", Copy_clipboard)
Map({ "n", "v", "x" }, "p", Paste_clipboard)
Map({ "n", "v", "x" }, "<C-s>", Save)
Map({ "n" }, "q", Close)

Map("v", "gs", Codesnap)
Map("v", "<", Outdent_vis)
Map("v", ">", Indent_vis)
Map("v", "gc", Comment_vis)

Map({ "n", "v" }, "zJ", Git_revert_change)
Map({ "n", "v" }, "zj", Git_stage_change)
-- Map({ "n", "v" }, "zt", Vscode_ctrl_d)
-- Map({ "n", "v" }, "zb", Vscode_ctrl_u)
```

## Config VSCode

settings.json

```json
{
  "workbench.iconTheme": "pcode-icon-theme-dark-spesifik",
  "editor.fontFamily": "'FiraCode Nerd Font'",
  "editor.fontSize": 16,
  "workbench.colorTheme": "Jetbrains Dracula Theme",
  "workbench.productIconTheme": "iconcarbon",
  "window.titleBarStyle": "custom",
  "workbench.activityBar.location": "top",
  "window.commandCenter": false,
  "window.menuBarVisibility": "compact",
  "workbench.startupEditor": "none",
  "extensions.experimental.affinity": {
    "asvetliakov.vscode-neovim": 1
  },
  // area custom whichkey mapping
  // remark mapping if don't want
  // edit mapping if you want
  // reference icon :
  // https://code.visualstudio.com/api/references/icons-in-labels#icon-listing
  "vspacecode.bindings": [
    {
      "key": " ",
      "name": "Commands",
      "icon": "rocket",
      "type": "command",
      "command": "workbench.action.showCommands"
    }
    // dst ... lengkapnya cek file settings.json
  ]
}
```

keybindings.json

```json
// Place your key bindings in this file to override the defaults
[
  // Trigger vspacecode in empty editor group
  {
    "key": "shift+space",
    "command": "vspacecode.space"
    // "when": "activeEditorGroupEmpty && focusedView == '' && !whichkeyActive && !inputFocus"
  },
  // Trigger vspacecode when sidebar is in focus
  {
    "key": "space",
    "command": "vspacecode.space",
    "when": "sideBarFocus && !inputFocus && !whichkeyActive"
  },
  // Keybindings required for edamagit
  // https://github.com/kahole/edamagit#vim-support-vscodevim
  // Cannot be added to package.json because keybinding replacements
  {
    "key": "tab",
    "command": "extension.vim_tab",
    "when": "editorTextFocus && vim.active && !inDebugRepl && vim.mode != 'Insert' && editorLangId != 'magit'"
  },
  {
    "key": "tab",
    "command": "-extension.vim_tab",
    "when": "editorTextFocus && vim.active && !inDebugRepl && vim.mode != 'Insert'"
  },
  {
    "key": "x",
    "command": "magit.discard-at-point",
    "when": "editorTextFocus && editorLangId == 'magit' && vim.mode =~ /^(?!SearchInProgressMode|CommandlineInProgress).*$/"
  },
  {
    "key": "k",
    "command": "-magit.discard-at-point"
  },
  {
    "key": "-",
    "command": "magit.reverse-at-point",
    "when": "editorTextFocus && editorLangId == 'magit' && vim.mode =~ /^(?!SearchInProgressMode|CommandlineInProgress).*$/"
  },
  {
    "key": "v",
    "command": "-magit.reverse-at-point"
  },
  {
    "key": "shift+-",
    "command": "magit.reverting",
    "when": "editorTextFocus && editorLangId == 'magit' && vim.mode =~ /^(?!SearchInProgressMode|CommandlineInProgress).*$/"
  },
  {
    "key": "shift+v",
    "command": "-magit.reverting"
  },
  {
    "key": "shift+o",
    "command": "magit.resetting",
    "when": "editorTextFocus && editorLangId == 'magit' && vim.mode =~ /^(?!SearchInProgressMode|CommandlineInProgress).*$/"
  },
  {
    "key": "shift+x",
    "command": "-magit.resetting"
  },
  {
    "key": "x",
    "command": "-magit.reset-mixed"
  },
  {
    "key": "ctrl+u x",
    "command": "-magit.reset-hard"
  },
  // Extra ref menu support for edamagit with the key "y"
  // Cannot be added to package.json because keybinding replacements
  {
    "key": "y",
    "command": "-magit.show-refs"
  },
  {
    "key": "y",
    "command": "vspacecode.showMagitRefMenu",
    "when": "editorTextFocus && editorLangId == 'magit' && vim.mode == 'Normal'"
  },
  // Extra refresh menu support for edamagit with the key "g"
  // Cannot be added to package.json because keybinding replacements
  {
    "key": "g",
    "command": "-magit.refresh",
    "when": "editorTextFocus && editorLangId == 'magit' && vim.mode =~ /^(?!SearchInProgressMode|CommandlineInProgress).*$/"
  },
  {
    "key": "g",
    "command": "vspacecode.showMagitRefreshMenu",
    "when": "editorTextFocus && editorLangId == 'magit' && vim.mode =~ /^(?!SearchInProgressMode|CommandlineInProgress).*$/"
  },
  // Easy navigation in quick open/QuickPick
  {
    "key": "ctrl+j",
    "command": "workbench.action.quickOpenSelectNext",
    "when": "inQuickOpen"
  },
  {
    "key": "ctrl+k",
    "command": "workbench.action.quickOpenSelectPrevious",
    "when": "inQuickOpen"
  },
  // Easy navigation in suggestion/intellisense
  // Cannot be added to package.json because of conflict with vim's default bindings
  {
    "key": "ctrl+j",
    "command": "selectNextSuggestion",
    "when": "suggestWidgetMultipleSuggestions && suggestWidgetVisible && textInputFocus"
  },
  {
    "key": "ctrl+k",
    "command": "selectPrevSuggestion",
    "when": "suggestWidgetMultipleSuggestions && suggestWidgetVisible && textInputFocus"
  },
  {
    "key": "ctrl+l",
    "command": "acceptSelectedSuggestion",
    "when": "suggestWidgetMultipleSuggestions && suggestWidgetVisible && textInputFocus"
  },
  // Easy navigation in parameter hint (i.e. traverse the hints when there's multiple overload for one method)
  // Cannot be added to package.json because of conflict with vim's default bindings
  {
    "key": "ctrl+j",
    "command": "showNextParameterHint",
    "when": "editorFocus && parameterHintsMultipleSignatures && parameterHintsVisible"
  },
  {
    "key": "ctrl+k",
    "command": "showPrevParameterHint",
    "when": "editorFocus && parameterHintsMultipleSignatures && parameterHintsVisible"
  },
  // Easy navigation in code action
  {
    "key": "ctrl+j",
    "command": "selectNextCodeAction",
    "when": "codeActionMenuVisible"
  },
  {
    "key": "ctrl+k",
    "command": "selectPrevCodeAction",
    "when": "codeActionMenuVisible"
  },
  {
    "key": "ctrl+l",
    "command": "acceptSelectedCodeAction",
    "when": "codeActionMenuVisible"
  },
  // Add ctrl+h/l to navigate in file browser
  {
    "key": "ctrl+h",
    "command": "file-browser.stepOut",
    "when": "inFileBrowser"
  },
  {
    "key": "ctrl+l",
    "command": "file-browser.stepIn",
    "when": "inFileBrowser"
  },

  // start custom mappings by pojok code
  // create new file base on focus
  {
    "key": "ctrl+n",
    "command": "explorer.newFile",
    "when": "explorerViewletFocus"
  },
  // create new folder base on focus
  {
    "key": "ctrl+shift+n",
    "command": "explorer.newFolder",
    "when": "explorerViewletFocus"
  },
  // navigate focus cursor down panel
  {
    "key": "ctrl+down",
    "command": "workbench.action.navigateDown"
  },
  // navigate focus cursor up panel
  {
    "key": "ctrl+up",
    "command": "workbench.action.navigateUp"
  },
  // navigate focus cursor left panel
  {
    "key": "ctrl+left",
    "command": "workbench.action.navigateLeft"
  },
  // navigate focus cursor tight panel
  {
    "key": "ctrl+right",
    "command": "workbench.action.navigateRight"
  },
  // view toggle panel visibility
  {
    "key": "ctrl+j",
    "command": "workbench.action.togglePanel"
  },
  // toggle primary side bar
  {
    "key": "ctrl+b",
    "command": "workbench.action.toggleSidebarVisibility"
  },
  // select all text in editor
  {
    "key": "ctrl+a",
    "command": "editor.action.selectAll"
  },
  // copy selected text in editor
  {
    "key": "ctrl+c",
    "command": "editor.action.clipboardCopyAction"
  },
  // paste selected text in editor
  {
    "key": "ctrl+v",
    "command": "editor.action.clipboardPasteAction"
  },
  // undo
  {
    "key": "ctrl+z",
    "command": "undo"
  },
  // redo
  {
    "key": "ctrl+shift+z",
    "command": "redo"
  },
  {
    "key": "ctrl+y",
    "command": "redo"
  },
  // indent line
  {
    "key": "ctrl+]",
    "command": "editor.action.indentLines"
  },
  // outdent line
  {
    "key": "ctrl+[",
    "command": "editor.action.outdentLines"
  },
  // copy line down
  {
    "key": "shift+alt+down",
    "command": "editor.action.copyLinesDownAction"
  },
  // copy line up
  {
    "key": "shift+alt+up",
    "command": "editor.action.copyLinesUpAction"
  },
  // close editor
  {
    "key": "ctrl+w q",
    "command": "workbench.action.closeActiveEditor"
  },
  // resize panel
  /* {
        "key": "ctrl+shift+o",
        "command": "workbench.action.decreaseViewSize"
      },
      {
        "key": "ctrl+shift+i",
        "command": "workbench.action.increaseViewSize"
      }, */
  // split terminal
  {
    "key": "ctrl+shift+t",
    "command": "workbench.action.terminal.split",
    "when": "terminalFocus"
  },
  // kill terminal focus
  {
    "key": "ctrl+shift+k",
    "command": "workbench.action.terminal.kill",
    "when": "terminalFocus"
  },
  // navigate split terminal
  // default alt + arrow key
  // increase height panel if terminal is open and terminal is focus
  {
    "key": "ctrl+shift+m",
    "command": "workbench.action.increaseViewHeight",
    "when": "terminalIsOpen && terminalFocus"
  },
  {
    "key": "ctrl+shift+p",
    "command": "workbench.action.decreaseViewHeight",
    "when": "terminalIsOpen && terminalFocus"
  },
  // increase width if sidebar is visible and sidebar is focus
  {
    "key": "ctrl+shift+m",
    "command": "workbench.action.increaseViewWidth",
    "when": "sideBarVisible && sideBarFocus"
  },
  {
    "key": "ctrl+shift+p",
    "command": "workbench.action.decreaseViewWidth",
    "when": "sideBarVisible && sideBarFocus"
  }
]
```
