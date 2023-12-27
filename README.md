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

function Center_screen()
	Cmd("call <SNR>3_reveal('center', 0)")
end

function Top_screen()
	Cmd("call <SNR>3_reveal('top', 0)")
end

function Bottom_screen()
	Cmd("call <SNR>3_reveal('bottom', 0)")
end

function Move_to_top_screen()
	Cmd("call <SNR>3_moveCursor('top')")
end

function Move_to_bottom_screen()
	Cmd("call <SNR>3_moveCursor('bottom')")
end

function Scroll_line_down()
	VSCodeCall("scrollLineDown")
end

function Scroll_line_up()
	VSCodeCall("scrollLineUp")
end

function Vscode_ctrl_d()
	VSCodeNotify("vscode-neovim.ctrl-d")
end

function Vscode_ctrl_u()
	VSCodeNotify("vscode-neovim.ctrl-u")
end

function Move_to_bottom_screen__center_screen()
	Move_to_bottom_screen()
	Center_screen()
end

function Move_to_top_screen__center_screen()
	Move_to_top_screen()
	Center_screen()
end

function Trim_trailing_whitespace()
	VSCodeCall("editor.action.trimTrailingWhitespace")
end

function Save()
	VSCodeCall("workbench.action.files.save")
end

function Save_no_format()
	VSCodeCall("workbench.action.files.saveWithoutFormatting")
end

function Trim__save__no_format()
	Trim_trailing_whitespace()
	Save_no_format()
end

function Trim__save__no_highlight()
	Trim_trailing_whitespace()
	Save()
	Remove_highlighting()
end

function Format()
	VSCodeCall("editor.action.formatDocument")
	print("formatted!")
end

function Trim__save__format()
	Trim_trailing_whitespace()
	Format()
	Save()
end

function Reveal_definition_aside()
	VSCodeNotify("editor.action.revealDefinitionAside")
end

function Go_to_implementation()
	VSCodeNotify("editor.action.goToImplementation")
end

function Go_to_reference()
	VSCodeNotify("editor.action.goToReferences")
end

function Rename_symbol()
	VSCodeNotify("editor.action.rename")
end

function Outdent()
	---@diagnostic disable-next-line: unused-local
	for i = 1, vim.v.count1 do
		VSCodeNotify("editor.action.outdentLines")
	end
end

function Indent()
	---@diagnostic disable-next-line: unused-local
	for i = 1, vim.v.count1 do
		VSCodeNotify("editor.action.indentLines")
	end
end

function Outdent_vis()
	VSCodeNotify("editor.action.outdentLines", false)
end

function Indent_vis()
	VSCodeNotify("editor.action.indentLines", false)
end

function Comment()
	VSCodeNotify("editor.action.commentLine")
end

function Convert_to_spaces()
	VSCodeNotify("editor.action.indentationToSpaces")
end

function Convert_to_tabs()
	VSCodeNotify("editor.action.indentationToTabs")
end

function Indent_with_spaces()
	VSCodeNotify("editor.action.indentUsingSpaces")
end

function Indent_with_tabs()
	VSCodeNotify("editor.action.indentUsingTabs")
end

function CloseEditor()
	VSCodeNotify("workbench.action.closeActiveEditor")
end

function UndoCloseEditor()
	VSCodeNotify("workbench.action.reopenClosedEditor")
end

function Git_stage_file()
	Trim_trailing_whitespace()
	Save()
	VSCodeNotify("git.stage")
end

function Git_unstage_file()
	Save()
	VSCodeNotify("git.unstage")
end

function Git_revert_change()
	VSCodeNotify("git.revertSelectedRanges")
end

function Git_stage_change()
	VSCodeNotify("git.stageSelectedRanges")
end

function Git_unstage_change()
	VSCodeNotify("git.unstageSelectedRanges")
end

function Git_open_changes()
	VSCodeNotify("git.openChange")
end

function Git_open_all_changes()
	VSCodeNotify("git.openAllChanges")
end

function Accept_merge_both()
	VSCodeNotify("merge-conflict.accept.both")
end

function Accept_merge_all_both()
	VSCodeNotify("merge-conflict.accept.all-both")
end

function Accept_merge_current()
	VSCodeNotify("merge-conflict.accept.current")
end

function Accept_merge_all_current()
	VSCodeNotify("merge-conflict.accept.all-current")
end

function Accept_merge_incoming()
	VSCodeNotify("merge-conflict.accept.incoming")
end

function Accept_merge_all_incoming()
	VSCodeNotify("merge-conflict.accept.all-incoming")
end

function Accept_merge_selection()
	VSCodeNotify("merge-conflict.accept.selection")
end

function Codesnap()
	VSCodeNotify("codesnap.start", true)
end

function Comment_vis()
	VSCodeNotify("editor.action.commentLine", false)
end

function Toggle_breakpoint()
	VSCodeNotify("editor.debug.action.toggleBreakpoint")
end

function Copy_path()
	VSCodeNotify("copyFilePath")
end

function Copy_relative_path()
	VSCodeNotify("copyRelativeFilePath")
end

function Navigation_down()
	VSCodeNotify("workbench.action.navigateDown")
end

function Navigation_up()
	VSCodeNotify("workbench.action.navigateUp")
end

function Navigation_left()
	VSCodeNotify("workbench.action.navigateLeft")
end

function Navigation_right()
	VSCodeNotify("workbench.action.navigateRight")
end

function Select_all()
	VSCodeNotify("editor.action.selectAll")
end

function Copy_clipboard()
	VSCodeNotify("editor.action.clipboardCopyAction")
end

function Paste_clipboard()
	VSCodeNotify("editor.action.clipboardPasteAction")
end

function Save()
	VSCodeNotify("workbench.action.files.save")
	VSCodeNotify("workbench.action.files.saveAll")
end

function Close()
	VSCodeNotify("workbench.action.closeActiveEditor")
end
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
		},
		{
			"key": "\t",
			"name": "Last buffer",
			"icon": "go-to-file",
			"type": "commands",
			"commands": [
				"workbench.action.quickOpenPreviousRecentlyUsedEditorInGroup",
				"list.select"
			]
		},
		{
			"key": "!",
			"name": "Show terminal",
			"icon": "terminal",
			"type": "command",
			"command": "workbench.action.terminal.focus"
		},
		{
			"key": "\"",
			"name": "Open new external terminal",
			"icon": "chevron-right",
			"type": "command",
			"command": "workbench.action.terminal.openNativeConsole"
		},
		{
			"key": "$",
			"name": "Run Recent Command in Terminal",
			"icon": "terminal",
			"type": "command",
			"command": "workbench.action.terminal.runRecentCommand"
		},
		{
			"key": "'",
			"name": "Show terminal",
			"icon": "terminal",
			"type": "command",
			"command": "workbench.action.terminal.focus"
		},
		{
			"key": "*",
			"name": "Search in project with selection",
			"icon": "search",
			"type": "commands",
			"commands": [
				"editor.action.addSelectionToNextFindMatch",
				"workbench.action.findInFiles",
				"search.action.focusSearchList"
			]
		},
		{
			"key": ".",
			"name": "Repeat most recent action",
			"icon": "redo",
			"type": "command",
			"command": "whichkey.repeatMostRecent",
			"args": "vspacecode.bindings"
		},
		{
			"key": "/",
			"name": "Search in project",
			"icon": "search",
			"type": "command",
			"command": "workbench.action.findInFiles"
		},
		{
			"key": "0",
			"name": "Focus on files explorer",
			"icon": "list-tree",
			"type": "command",
			"command": "workbench.files.action.focusFilesExplorer"
		},
		{
			"key": "1",
			"name": "Focus 1st window",
			"icon": "files",
			"type": "command",
			"command": "workbench.action.focusFirstEditorGroup"
		},
		{
			"key": "2",
			"name": "Focus 2nd window",
			"icon": "files",
			"type": "command",
			"command": "workbench.action.focusSecondEditorGroup"
		},
		{
			"key": "3",
			"name": "Focus 3rd window",
			"icon": "files",
			"type": "command",
			"command": "workbench.action.focusThirdEditorGroup"
		},
		{
			"key": "4",
			"name": "Focus 4th window",
			"icon": "files",
			"type": "command",
			"command": "workbench.action.focusFourthEditorGroup"
		},
		{
			"key": "5",
			"name": "Focus 5th window",
			"icon": "files",
			"type": "command",
			"command": "workbench.action.focusFifthEditorGroup"
		},
		{
			"key": "6",
			"name": "Focus 6th window",
			"icon": "files",
			"type": "command",
			"command": "workbench.action.focusSixthEditorGroup"
		},
		{
			"key": "7",
			"name": "Focus 7th window",
			"icon": "files",
			"type": "command",
			"command": "workbench.action.focusSeventhEditorGroup"
		},
		{
			"key": "8",
			"name": "Focus 8th window",
			"icon": "files",
			"type": "command",
			"command": "workbench.action.focusEighthEditorGroup"
		},
		{
			"key": ";",
			"name": "Toggle comment",
			"icon": "comment",
			"type": "command",
			"command": "editor.action.commentLine"
		},
		{
			"key": "?",
			"name": "Search keybindings",
			"icon": "keyboard",
			"type": "command",
			"command": "whichkey.searchBindings"
		},
		{
			"key": "v",
			"name": "Smart select/expand region",
			"icon": "selection",
			"type": "transient",
			"command": "editor.action.smartSelect.grow",
			"bindings": [
				{
					"key": "v",
					"name": "Grow selection",
					"icon": "add",
					"type": "command",
					"command": "editor.action.smartSelect.grow"
				},
				{
					"key": "V",
					"name": "Shrink selection",
					"icon": "remove",
					"type": "command",
					"command": "editor.action.smartSelect.shrink"
				}
			]
		},
		{
			"key": ":",
			"name": "+Tasks",
			"icon": "tasklist",
			"type": "bindings",
			"bindings": [
				{
					"key": ".",
					"name": "Rerun last task",
					"icon": "debug-rerun",
					"type": "command",
					"command": "workbench.action.tasks.reRunTask"
				},
				{
					"key": ":",
					"name": "Run task",
					"icon": "play",
					"type": "command",
					"command": "workbench.action.tasks.runTask"
				},
				{
					"key": "b",
					"name": "Run build tasks",
					"icon": "server-process",
					"type": "command",
					"command": "workbench.action.tasks.build"
				},
				{
					"key": "c",
					"name": "Configure task runner",
					"icon": "gear",
					"type": "command",
					"command": "workbench.action.tasks.configureTaskRunner"
				},
				{
					"key": "g",
					"name": "Show running tasks",
					"icon": "checklist",
					"type": "command",
					"command": "workbench.action.tasks.showTasks"
				},
				{
					"key": "l",
					"name": "Show task log",
					"icon": "history",
					"type": "command",
					"command": "workbench.action.tasks.showLog"
				},
				{
					"key": "t",
					"name": "Run test task",
					"icon": "beaker",
					"type": "command",
					"command": "workbench.action.tasks.test"
				},
				{
					"key": "x",
					"name": "Terminate task",
					"icon": "trash",
					"type": "command",
					"command": "workbench.action.tasks.terminate"
				},
				{
					"key": "R",
					"name": "Restart running task",
					"icon": "refresh",
					"type": "command",
					"command": "workbench.action.tasks.restartTask"
				}
			]
		},
		{
			"key": "b",
			"name": "+Buffers",
			"icon": "file",
			"type": "bindings",
			"bindings": [
				{
					"key": "0",
					"name": "Last buffer in window",
					"icon": "arrow-both",
					"type": "command",
					"command": "workbench.action.lastEditorInGroup"
				},
				{
					"key": "1",
					"name": "First buffer in window",
					"icon": "arrow-both",
					"type": "command",
					"command": "workbench.action.openEditorAtIndex1"
				},
				{
					"key": "2",
					"name": "2nd buffer in window",
					"icon": "arrow-both",
					"type": "command",
					"command": "workbench.action.openEditorAtIndex2"
				},
				{
					"key": "3",
					"name": "3rd buffer in window",
					"icon": "arrow-both",
					"type": "command",
					"command": "workbench.action.openEditorAtIndex3"
				},
				{
					"key": "4",
					"name": "4th buffer in window",
					"icon": "arrow-both",
					"type": "command",
					"command": "workbench.action.openEditorAtIndex4"
				},
				{
					"key": "5",
					"name": "5th buffer in window",
					"icon": "arrow-both",
					"type": "command",
					"command": "workbench.action.openEditorAtIndex5"
				},
				{
					"key": "6",
					"name": "6th buffer in window",
					"icon": "arrow-both",
					"type": "command",
					"command": "workbench.action.openEditorAtIndex6"
				},
				{
					"key": "7",
					"name": "7th buffer in window",
					"icon": "arrow-both",
					"type": "command",
					"command": "workbench.action.openEditorAtIndex7"
				},
				{
					"key": "8",
					"name": "8th buffer in window",
					"icon": "arrow-both",
					"type": "command",
					"command": "workbench.action.openEditorAtIndex8"
				},
				{
					"key": "9",
					"name": "9th buffer in window",
					"icon": "arrow-both",
					"type": "command",
					"command": "workbench.action.openEditorAtIndex9"
				},
				{
					"key": "b",
					"name": "Show all buffers",
					"icon": "files",
					"type": "command",
					"command": "workbench.action.showAllEditorsByMostRecentlyUsed"
				},
				{
					"key": "d",
					"name": "Close active buffer",
					"icon": "x",
					"type": "command",
					"command": "workbench.action.closeActiveEditor"
				},
				{
					"key": "h",
					"name": "Move buffer into left window",
					"icon": "triangle-left",
					"type": "command",
					"command": "workbench.action.moveEditorToLeftGroup"
				},
				{
					"key": "j",
					"name": "Move buffer into below window",
					"icon": "triangle-down",
					"type": "command",
					"command": "workbench.action.moveEditorToBelowGroup"
				},
				{
					"key": "k",
					"name": "Move buffer into above window",
					"icon": "triangle-up",
					"type": "command",
					"command": "workbench.action.moveEditorToAboveGroup"
				},
				{
					"key": "l",
					"name": "Move buffer into right window",
					"icon": "triangle-right",
					"type": "command",
					"command": "workbench.action.moveEditorToRightGroup"
				},
				{
					"key": "n",
					"name": "Next buffer",
					"icon": "arrow-down",
					"type": "command",
					"command": "workbench.action.nextEditor"
				},
				{
					"key": "p",
					"name": "Previous buffer",
					"icon": "arrow-up",
					"type": "command",
					"command": "workbench.action.previousEditor"
				},
				{
					"key": "s",
					"name": "Scratch buffer",
					"icon": "note",
					"type": "command",
					"command": "workbench.action.files.newUntitledFile"
				},
				{
					"key": "t",
					"name": "Pin buffer",
					"icon": "pin",
					"type": "command",
					"command": "workbench.action.pinEditor"
				},
				{
					"key": "u",
					"name": "Reopen closed buffer",
					"icon": "history",
					"type": "command",
					"command": "workbench.action.reopenClosedEditor"
				},
				{
					"key": "B",
					"name": "Show all buffers in active window",
					"icon": "files",
					"type": "command",
					"command": "workbench.action.showEditorsInActiveGroup"
				},
				{
					"key": "H",
					"name": "Move buffer into left window",
					"icon": "triangle-left",
					"type": "command",
					"command": "workbench.action.moveEditorToLeftGroup"
				},
				{
					"key": "J",
					"name": "Move buffer into below window",
					"icon": "triangle-down",
					"type": "command",
					"command": "workbench.action.moveEditorToBelowGroup"
				},
				{
					"key": "K",
					"name": "Move buffer into above window",
					"icon": "triangle-up",
					"type": "command",
					"command": "workbench.action.moveEditorToAboveGroup"
				},
				{
					"key": "L",
					"name": "Move buffer into right window",
					"icon": "triangle-right",
					"type": "command",
					"command": "workbench.action.moveEditorToRightGroup"
				},
				{
					"key": "M",
					"name": "Close other buffers",
					"icon": "close-all",
					"type": "command",
					"command": "workbench.action.closeOtherEditors"
				},
				{
					"key": "P",
					"name": "Paste clipboard to buffer",
					"icon": "clippy",
					"type": "commands",
					"commands": [
						"editor.action.selectAll",
						"editor.action.clipboardPasteAction"
					]
				},
				{
					"key": "R",
					"name": "Revert the current buffer",
					"icon": "discard",
					"type": "command",
					"command": "workbench.action.files.revert"
				},
				{
					"key": "T",
					"name": "Unpin buffer",
					"icon": "pinned",
					"type": "command",
					"command": "workbench.action.unpinEditor"
				},
				{
					"key": "Y",
					"name": "Copy buffer to clipboard",
					"icon": "clippy",
					"type": "command",
					"command": "vspacecode.copyWholeBuffer"
				},
				{
					"key": "N",
					"name": "+New Buffer",
					"icon": "file-add",
					"type": "bindings",
					"bindings": [
						{
							"key": "h",
							"name": "New untitled buffer (split left)",
							"icon": "arrow-small-left",
							"type": "commands",
							"commands": [
								"workbench.action.splitEditorLeft",
								"workbench.action.files.newUntitledFile",
								"workbench.action.closeOtherEditors"
							]
						},
						{
							"key": "j",
							"name": "New untitled buffer (split down)",
							"icon": "arrow-small-down",
							"type": "commands",
							"commands": [
								"workbench.action.splitEditorDown",
								"workbench.action.files.newUntitledFile",
								"workbench.action.closeOtherEditors"
							]
						},
						{
							"key": "k",
							"name": "New untitled buffer (split up)",
							"icon": "arrow-small-up",
							"type": "commands",
							"commands": [
								"workbench.action.splitEditorUp",
								"workbench.action.files.newUntitledFile",
								"workbench.action.closeOtherEditors"
							]
						},
						{
							"key": "l",
							"name": "New untitled buffer (split right)",
							"icon": "arrow-small-right",
							"type": "commands",
							"commands": [
								"workbench.action.splitEditorRight",
								"workbench.action.files.newUntitledFile",
								"workbench.action.closeOtherEditors"
							]
						},
						{
							"key": "n",
							"name": "New untitled buffer",
							"icon": "file-add",
							"type": "command",
							"command": "workbench.action.files.newUntitledFile"
						}
					]
				}
			]
		},
		{
			"key": "c",
			"name": "+Compile/Comments",
			"icon": "gear",
			"type": "bindings",
			"bindings": [
				{
					"key": "c",
					"name": "Compile project",
					"icon": "gear",
					"type": "command",
					"command": "workbench.action.tasks.build"
				},
				{
					"key": "l",
					"name": "Toggle line comment",
					"icon": "comment",
					"type": "command",
					"command": "editor.action.commentLine"
				},
				{
					"key": "n",
					"name": "Next error",
					"icon": "arrow-down",
					"type": "command",
					"command": "editor.action.marker.nextInFiles"
				},
				{
					"key": "N",
					"name": "Previous error",
					"icon": "arrow-up",
					"type": "command",
					"command": "editor.action.marker.prevInFiles"
				}
			]
		},
		{
			"key": "d",
			"name": "+Debug",
			"icon": "bug",
			"type": "bindings",
			"bindings": [
				{
					"key": "c",
					"name": "Continue debug",
					"icon": "debug-continue",
					"type": "command",
					"command": "workbench.action.debug.continue"
				},
				{
					"key": "d",
					"name": "Start debug",
					"icon": "debug-start",
					"type": "command",
					"command": "workbench.action.debug.start"
				},
				{
					"key": "i",
					"name": "Step into",
					"icon": "debug-step-into",
					"type": "command",
					"command": "workbench.action.debug.stepInto"
				},
				{
					"key": "j",
					"name": "Jump to cursor",
					"icon": "whole-word",
					"type": "command",
					"command": "debug.jumpToCursor"
				},
				{
					"key": "o",
					"name": "Step out",
					"icon": "debug-step-out",
					"type": "command",
					"command": "workbench.action.debug.stepOut"
				},
				{
					"key": "p",
					"name": "Pause debug",
					"icon": "debug-pause",
					"type": "command",
					"command": "workbench.action.debug.pause"
				},
				{
					"key": "s",
					"name": "Step over",
					"icon": "debug-step-over",
					"type": "command",
					"command": "workbench.action.debug.stepOver"
				},
				{
					"key": "v",
					"name": "REPL",
					"icon": "debug-console",
					"type": "command",
					"command": "workbench.debug.action.toggleRepl"
				},
				{
					"key": "w",
					"name": "Focus on watch window",
					"icon": "eye-watch",
					"type": "command",
					"command": "workbench.debug.action.focusWatchView"
				},
				{
					"key": "C",
					"name": "Continue to cursor",
					"icon": "debug-continue",
					"type": "command",
					"command": "editor.debug.action.runToCursor"
				},
				{
					"key": "D",
					"name": "Run without debugging",
					"icon": "run",
					"type": "command",
					"command": "workbench.action.debug.run"
				},
				{
					"key": "R",
					"name": "Restart debug",
					"icon": "debug-restart",
					"type": "command",
					"command": "workbench.action.debug.restart"
				},
				{
					"key": "S",
					"name": "Stop debug",
					"icon": "debug-stop",
					"type": "command",
					"command": "workbench.action.debug.stop"
				},
				{
					"key": "W",
					"name": "Add to watch",
					"icon": "watch-expressions-add",
					"type": "command",
					"command": "editor.debug.action.selectionToWatch"
				},
				{
					"key": "b",
					"name": "+Breakpoint",
					"icon": "debug-breakpoint",
					"type": "bindings",
					"bindings": [
						{
							"key": "b",
							"name": "Toggle breakpoint",
							"icon": "activate-breakpoints",
							"type": "command",
							"command": "editor.debug.action.toggleBreakpoint"
						},
						{
							"key": "c",
							"name": "Add conditional breakpoint",
							"icon": "debug-breakpoint-conditional",
							"type": "command",
							"command": "editor.debug.action.conditionalBreakpoint"
						},
						{
							"key": "d",
							"name": "Delete breakpoint",
							"icon": "trash",
							"type": "command",
							"command": "debug.removeBreakpoint"
						},
						{
							"key": "e",
							"name": "Enable breakpoint",
							"icon": "debug-breakpoint",
							"type": "command",
							"command": "debug.enableOrDisableBreakpoint"
						},
						{
							"key": "f",
							"name": "Add function breakpoint",
							"icon": "debug-breakpoint-function",
							"type": "command",
							"command": "workbench.debug.viewlet.action.addFunctionBreakpointAction"
						},
						{
							"key": "i",
							"name": "Toggle inline breakpoint",
							"icon": "activate-breakpoints",
							"type": "command",
							"command": "editor.debug.action.toggleInlineBreakpoint"
						},
						{
							"key": "n",
							"name": "Next breakpoint",
							"icon": "arrow-down",
							"type": "transient",
							"command": "editor.debug.action.goToNextBreakpoint",
							"bindings": [
								{
									"key": "n",
									"name": "Next breakpoint",
									"icon": "arrow-down",
									"type": "command",
									"command": "editor.debug.action.goToNextBreakpoint"
								},
								{
									"key": "p",
									"name": "Previous breakpoint",
									"icon": "arrow-up",
									"type": "command",
									"command": "editor.debug.action.goToPreviousBreakpoint"
								}
							]
						},
						{
							"key": "p",
							"name": "Previous breakpoint",
							"icon": "arrow-up",
							"type": "transient",
							"command": "editor.debug.action.goToPreviousBreakpoint",
							"bindings": [
								{
									"key": "n",
									"name": "Next breakpoint",
									"icon": "arrow-down",
									"type": "command",
									"command": "editor.debug.action.goToNextBreakpoint"
								},
								{
									"key": "p",
									"name": "Previous breakpoint",
									"icon": "arrow-up",
									"type": "command",
									"command": "editor.debug.action.goToPreviousBreakpoint"
								}
							]
						},
						{
							"key": "s",
							"name": "Disable breakpoint",
							"icon": "debug-breakpoint-disabled",
							"type": "command",
							"command": "debug.enableOrDisableBreakpoint"
						},
						{
							"key": "D",
							"name": "Delete all breakpoints",
							"icon": "trash",
							"type": "command",
							"command": "workbench.debug.viewlet.action.removeAllBreakpoints"
						},
						{
							"key": "E",
							"name": "Enable all breakpoints",
							"icon": "expand-all",
							"type": "command",
							"command": "workbench.debug.viewlet.action.enableAllBreakpoints"
						},
						{
							"key": "S",
							"name": "Disable all breakpoints",
							"icon": "collapse-all",
							"type": "command",
							"command": "workbench.debug.viewlet.action.disableAllBreakpoints"
						}
					]
				}
			]
		},
		{
			"key": "e",
			"name": "+Errors",
			"icon": "error",
			"type": "bindings",
			"bindings": [
				{
					"key": ".",
					"name": "Error transient",
					"icon": "window",
					"type": "transient",
					"bindings": [
						{
							"key": "f",
							"name": "Fix error",
							"icon": "lightbulb-autofix",
							"type": "command",
							"command": "editor.action.quickFix"
						},
						{
							"key": "n",
							"name": "Next error",
							"icon": "arrow-down",
							"type": "command",
							"command": "editor.action.marker.nextInFiles"
						},
						{
							"key": "p",
							"name": "Previous error",
							"icon": "arrow-up",
							"type": "command",
							"command": "editor.action.marker.prevInFiles"
						},
						{
							"key": "N",
							"name": "Previous error",
							"icon": "arrow-up",
							"type": "command",
							"command": "editor.action.marker.prevInFiles"
						}
					]
				},
				{
					"key": "e",
					"name": "Show error",
					"icon": "error",
					"type": "command",
					"command": "editor.action.showHover"
				},
				{
					"key": "f",
					"name": "Fix error",
					"icon": "lightbulb-autofix",
					"type": "command",
					"command": "editor.action.quickFix"
				},
				{
					"key": "l",
					"name": "List errors",
					"icon": "list-flat",
					"type": "command",
					"command": "workbench.actions.view.problems"
				},
				{
					"key": "n",
					"name": "Next error",
					"icon": "arrow-down",
					"type": "command",
					"command": "editor.action.marker.nextInFiles"
				},
				{
					"key": "p",
					"name": "Previous error",
					"icon": "arrow-up",
					"type": "command",
					"command": "editor.action.marker.prevInFiles"
				},
				{
					"key": "N",
					"name": "Previous error",
					"icon": "arrow-up",
					"type": "command",
					"command": "editor.action.marker.prevInFiles"
				}
			]
		},
		{
			"key": "f",
			"name": "+File",
			"icon": "file",
			"type": "bindings",
			"bindings": [
				{
					"key": "f",
					"name": "Open file/folder",
					"icon": "folder-opened",
					"type": "command",
					"command": "file-browser.open"
				},
				{
					"key": "l",
					"name": "Change file language",
					"icon": "code",
					"type": "command",
					"command": "workbench.action.editor.changeLanguageMode"
				},
				{
					"key": "n",
					"name": "New file",
					"icon": "new-file",
					"type": "command",
					"command": "explorer.newFile"
				},
				{
					"key": "o",
					"name": "+Open with",
					"icon": "file-code",
					"type": "command",
					"command": "explorer.openWith"
				},
				{
					"key": "r",
					"name": "+Open recent",
					"icon": "clock",
					"type": "command",
					"command": "workbench.action.openRecent"
				},
				{
					"key": "s",
					"name": "Save file",
					"icon": "save",
					"type": "command",
					"command": "workbench.action.files.save"
				},
				{
					"key": "t",
					"name": "Toggle tree/explorer view",
					"icon": "list-tree",
					"type": "conditional",
					"bindings": [
						{
							"key": "",
							"name": "Show explorer view",
							"type": "command",
							"command": "workbench.view.explorer"
						},
						{
							"key": "when:sideBarVisible && explorerViewletVisible",
							"name": "Hide side bar",
							"type": "command",
							"command": "workbench.action.toggleSidebarVisibility"
						}
					]
				},
				{
					"key": "w",
					"name": "Open active in new window",
					"icon": "window",
					"type": "command",
					"command": "workbench.action.files.showOpenedFileInNewWindow"
				},
				{
					"key": "D",
					"name": "Delete current file",
					"icon": "trash",
					"type": "commands",
					"commands": [
						"workbench.files.action.showActiveFileInExplorer",
						"deleteFile"
					]
				},
				{
					"key": "L",
					"name": "Locate file",
					"icon": "file-symlink-directory",
					"type": "command",
					"command": "revealFileInOS"
				},
				{
					"key": "R",
					"name": "Rename file",
					"icon": "edit",
					"type": "commands",
					"commands": [
						"revealInExplorer",
						"renameFile"
					]
				},
				{
					"key": "S",
					"name": "Save all files",
					"icon": "save-all",
					"type": "command",
					"command": "workbench.action.files.saveAll"
				},
				{
					"key": "T",
					"name": "Show active file in tree/explorer view",
					"icon": "list-tree",
					"type": "command",
					"command": "workbench.files.action.showActiveFileInExplorer"
				},
				{
					"key": "e",
					"name": "+Emacs/VSpaceCode",
					"icon": "settings",
					"type": "bindings",
					"bindings": [
						{
							"key": "d",
							"name": "Open settings",
							"icon": "settings",
							"type": "command",
							"command": "workbench.action.openGlobalSettings"
						},
						{
							"key": "k",
							"name": "Open global key bindings",
							"icon": "keyboard",
							"type": "command",
							"command": "workbench.action.openGlobalKeybindings"
						},
						{
							"key": "l",
							"name": "Open language settings",
							"icon": "code",
							"type": "command",
							"command": "workbench.action.configureLanguageBasedSettings"
						},
						{
							"key": "s",
							"name": "Configure user snippets",
							"icon": "symbol-snippet",
							"type": "command",
							"command": "workbench.action.openSnippets"
						},
						{
							"key": "w",
							"name": "Open workspace settings",
							"icon": "settings-edit",
							"type": "command",
							"command": "workbench.action.openWorkspaceSettings"
						},
						{
							"key": "D",
							"name": "Open settings JSON",
							"icon": "json",
							"type": "command",
							"command": "workbench.action.openSettingsJson"
						},
						{
							"key": "K",
							"name": "Open global key bindings JSON",
							"icon": "json",
							"type": "command",
							"command": "workbench.action.openGlobalKeybindingsFile"
						},
						{
							"key": "W",
							"name": "Open workspace settings JSON",
							"icon": "json",
							"type": "command",
							"command": "workbench.action.openWorkspaceSettingsFile"
						}
					]
				},
				{
					"key": "i",
					"name": "+Indentation",
					"icon": "arrow-right",
					"type": "bindings",
					"bindings": [
						{
							"key": "d",
							"name": "Detect indentation",
							"icon": "whitespace",
							"type": "command",
							"command": "editor.action.detectIndentation"
						},
						{
							"key": "i",
							"name": "Change indentation",
							"icon": "edit",
							"type": "command",
							"command": "changeEditorIndentation"
						},
						{
							"key": "r",
							"name": "Reindent",
							"icon": "list-flat",
							"type": "command",
							"command": "editor.action.reindentlines"
						},
						{
							"key": "s",
							"name": "Convert indentation to spaces",
							"icon": "arrow-small-right",
							"type": "command",
							"command": "editor.action.indentationToSpaces"
						},
						{
							"key": "t",
							"name": "Convert indentation to tabs",
							"icon": "export",
							"type": "command",
							"command": "editor.action.indentationToTabs"
						},
						{
							"key": "R",
							"name": "Reindent selected",
							"icon": "selection",
							"type": "command",
							"command": "editor.action.reindentselectedlines"
						}
					]
				},
				{
					"key": "y",
					"name": "+Yank",
					"icon": "clippy",
					"type": "bindings",
					"bindings": [
						{
							"key": "c",
							"name": "Copy path of active file with line and column",
							"icon": "list-selection",
							"type": "command",
							"command": "vspacecode.copyPathWithLineColumn"
						},
						{
							"key": "d",
							"name": "Copy directory path of the active file",
							"icon": "file-directory",
							"type": "command",
							"command": "vspacecode.copyDirectoryPath"
						},
						{
							"key": "l",
							"name": "Copy path of active file with line",
							"icon": "list-flat",
							"type": "command",
							"command": "vspacecode.copyPathWithLine"
						},
						{
							"key": "n",
							"name": "Copy filename of active file",
							"icon": "file",
							"type": "command",
							"command": "vspacecode.copyFilename"
						},
						{
							"key": "y",
							"name": "Copy path of active file",
							"icon": "go-to-file",
							"type": "command",
							"command": "vspacecode.copyPath"
						},
						{
							"key": "C",
							"name": "Copy relative path of active file with line and column",
							"icon": "list-selection",
							"type": "command",
							"command": "vspacecode.copyRelativePathWithLineColumn"
						},
						{
							"key": "D",
							"name": "Copy relative directory path of the active file",
							"icon": "file-directory",
							"type": "command",
							"command": "vspacecode.copyRelativeDirectoryPath"
						},
						{
							"key": "L",
							"name": "Copy relative path of active file with line",
							"icon": "list-flat",
							"type": "command",
							"command": "vspacecode.copyRelativePathWithLine"
						},
						{
							"key": "N",
							"name": "Copy filename without extension of active file",
							"icon": "file",
							"type": "command",
							"command": "vspacecode.copyFilenameBase"
						},
						{
							"key": "Y",
							"name": "Copy relative path of active file",
							"icon": "go-to-file",
							"type": "command",
							"command": "vspacecode.copyRelativePath"
						}
					]
				}
			]
		},
		{
			"key": "g",
			"name": "+Git",
			"icon": "git-branch",
			"type": "bindings",
			"bindings": [
				{
					"key": "b",
					"name": "Blame file",
					"icon": "file",
					"type": "command",
					"command": "magit.blame-file"
				},
				{
					"key": "c",
					"name": "Clone",
					"icon": "repo-clone",
					"type": "command",
					"command": "git.clone"
				},
				{
					"key": "i",
					"name": "Initialize repository",
					"icon": "repo-create",
					"type": "command",
					"command": "git.init"
				},
				{
					"key": "m",
					"name": "Magit dispatch",
					"icon": "repo",
					"type": "command",
					"command": "magit.dispatch"
				},
				{
					"key": "s",
					"name": "Status",
					"icon": "preview",
					"type": "command",
					"command": "magit.status"
				},
				{
					"key": "S",
					"name": "Stage file",
					"icon": "file-add",
					"type": "command",
					"command": "magit.stage-file"
				},
				{
					"key": "U",
					"name": "Unstage file",
					"icon": "file",
					"type": "command",
					"command": "magit.unstage-file"
				},
				{
					"key": "f",
					"name": "+File",
					"icon": "file",
					"type": "bindings",
					"bindings": [
						{
							"key": "d",
							"name": "Diff",
							"icon": "diff",
							"type": "command",
							"command": "magit.diff-file"
						},
						{
							"key": "l",
							"name": "Show log/timeline",
							"icon": "history",
							"type": "command",
							"command": "timeline.focus"
						}
					]
				}
			]
		},
		{
			"key": "h",
			"name": "+Help",
			"icon": "question",
			"type": "bindings",
			"bindings": [
				{
					"key": "d",
					"name": "Open VSCode Documentation",
					"icon": "book",
					"type": "command",
					"command": "workbench.action.openDocumentationUrl"
				},
				{
					"key": "k",
					"name": "Open global key bindings",
					"icon": "keyboard",
					"type": "command",
					"command": "workbench.action.openGlobalKeybindings"
				},
				{
					"key": "D",
					"name": "Open VSpaceCode Documentation",
					"icon": "book",
					"type": "command",
					"command": "vspacecode.openDocumentationUrl"
				},
				{
					"key": "I",
					"name": "Report VSCode Issue",
					"icon": "issues",
					"type": "command",
					"command": "workbench.action.openIssueReporter"
				},
				{
					"key": "T",
					"name": "Open VSCode Tutorial",
					"icon": "lightbulb",
					"type": "command",
					"command": "workbench.action.showInteractivePlayground"
				}
			]
		},
		{
			"key": "i",
			"name": "+Insert",
			"icon": "add",
			"type": "bindings",
			"bindings": [
				{
					"key": "j",
					"name": "Insert line below",
					"icon": "arrow-down",
					"type": "command",
					"command": "editor.action.insertLineAfter"
				},
				{
					"key": "k",
					"name": "Insert line above",
					"icon": "arrow-up",
					"type": "command",
					"command": "editor.action.insertLineBefore"
				},
				{
					"key": "s",
					"name": "Insert snippet",
					"icon": "symbol-snippet",
					"type": "command",
					"command": "editor.action.insertSnippet"
				}
			]
		},
		{
			"key": "j",
			"name": "+Jump/Join/Split",
			"icon": "gather",
			"type": "bindings",
			"bindings": [
				{
					"key": "+",
					"name": "Format buffer",
					"icon": "file",
					"type": "command",
					"command": "editor.action.formatDocument"
				},
				{
					"key": "=",
					"name": "Format region or buffer",
					"icon": "list-flat",
					"type": "command",
					"command": "editor.action.format"
				},
				{
					"key": "c",
					"name": "Jump to previous change",
					"icon": "arrow-up",
					"type": "command",
					"command": "workbench.action.editor.previousChange"
				},
				{
					"key": "i",
					"name": "Jump to symbol in buffer",
					"icon": "symbol-class",
					"type": "command",
					"command": "workbench.action.gotoSymbol"
				},
				{
					"key": "j",
					"name": "Jump to character",
					"icon": "case-sensitive",
					"type": "command",
					"command": "vim.remap",
					"args": {
						"after": [
							"leader",
							"leader",
							"s"
						]
					}
				},
				{
					"key": "l",
					"name": "Jump to line",
					"icon": "list-flat",
					"type": "command",
					"command": "vim.remap",
					"args": {
						"after": [
							"leader",
							"leader",
							"leader",
							"b",
							"d",
							"j",
							"k"
						]
					}
				},
				{
					"key": "n",
					"name": "Split new line",
					"icon": "whitespace",
					"type": "command",
					"command": "lineBreakInsert"
				},
				{
					"key": "v",
					"name": "Jump to outline/variables",
					"icon": "variable",
					"type": "command",
					"command": "breadcrumbs.focusAndSelect"
				},
				{
					"key": "w",
					"name": "Jump to word",
					"icon": "symbol-keyword",
					"type": "command",
					"command": "vim.remap",
					"args": {
						"after": [
							"leader",
							"leader",
							"leader",
							"b",
							"d",
							"w"
						]
					}
				},
				{
					"key": "C",
					"name": "Jump to next change",
					"icon": "arrow-down",
					"type": "command",
					"command": "workbench.action.editor.nextChange"
				},
				{
					"key": "I",
					"name": "Jump to symbol in project",
					"icon": "project",
					"type": "command",
					"command": "workbench.action.showAllSymbols"
				}
			]
		},
		{
			"key": "l",
			"name": "+Layouts",
			"icon": "editor-layout",
			"type": "bindings",
			"bindings": [
				{
					"key": "d",
					"name": "Close workspace",
					"icon": "close-all",
					"type": "command",
					"command": "workbench.action.closeFolder"
				}
			]
		},
		{
			"key": "m",
			"name": "+Major",
			"icon": "code",
			"type": "conditional",
			"bindings": [
				{
					"key": "languageId:agda",
					"name": "Agda",
					"type": "bindings",
					"bindings": [
						{
							"key": ",",
							"name": "Show goal type and context (simplified)",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.goal-type-and-context[Simplified]"
						},
						{
							"key": ".",
							"name": "Show goal type, context and inferred type (simplified)",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.goal-type-context-and-inferred-type[Simplified]"
						},
						{
							"key": "=",
							"name": "Show constraints",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.show-constraints"
						},
						{
							"key": "?",
							"name": "Show all goals",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.show-goals"
						},
						{
							"key": "a",
							"name": "Automatic proof search",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.auto"
						},
						{
							"key": "b",
							"name": "Move to previous goal",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.previous-goal"
						},
						{
							"key": "c",
							"name": "Case split",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.case"
						},
						{
							"key": "d",
							"name": "Infer type (simplified)",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.infer-type[Simplified]"
						},
						{
							"key": "e",
							"name": "Show context (simplified)",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.context[Simplified]"
						},
						{
							"key": "f",
							"name": "Move to next goal",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.next-goal"
						},
						{
							"key": "h",
							"name": "Show helper function type (simplified)",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.helper-function-type[Simplified]"
						},
						{
							"key": "l",
							"name": "Load file",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.load"
						},
						{
							"key": "n",
							"name": "Compute normal form (simplified)",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.compute-normal-form[DefaultCompute]"
						},
						{
							"key": "r",
							"name": "Refine",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.refine"
						},
						{
							"key": "s",
							"name": "Solve constraints (simplified)",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.solve-constraints[Simplified]"
						},
						{
							"key": "t",
							"name": "Show goal type (simplified)",
							"icon": "repl",
							"type": "command",
							"command": "agda-mode.goal-type[Simplified]"
						},
						{
							"key": "w",
							"name": "Why in scope",
							"icon": "repl",
							"type": "bindings",
							"command": "agda-mode.why-in-scope"
						},
						{
							"key": "x",
							"name": "+Backend",
							"icon": "repl",
							"type": "bindings",
							"bindings": [
								{
									"key": "c",
									"name": "Compile module",
									"icon": "repl",
									"type": "command",
									"command": "agda-mode.compile"
								},
								{
									"key": "h",
									"name": "Toggle display of implicit arguments",
									"icon": "repl",
									"type": "command",
									"command": "agda-mode.toggle-display-of-implicit-arguments"
								},
								{
									"key": "q",
									"name": "Quit",
									"icon": "repl",
									"type": "command",
									"command": "agda-mode.quit"
								},
								{
									"key": "r",
									"name": "Restart",
									"icon": "repl",
									"type": "command",
									"command": "agda-mode.restart"
								}
							]
						}
					]
				},
				{
					"key": "languageId:clojure",
					"name": "Clojure",
					"type": "bindings",
					"bindings": [
						{
							"key": "!",
							"name": "Disconnect from REPL",
							"icon": "debug-disconnect",
							"type": "command",
							"command": "calva.disconnect"
						},
						{
							"key": "\"",
							"name": "Jack-in to REPL",
							"icon": "repl",
							"type": "command",
							"command": "calva.jackIn"
						},
						{
							"key": "'",
							"name": "Connect to REPL",
							"icon": "repl",
							"type": "command",
							"command": "calva.connect"
						},
						{
							"key": ".",
							"name": "Connect or jack-in",
							"icon": "repl",
							"type": "command",
							"command": "calva.jackInOrConnect"
						},
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format current form",
									"icon": "list-selection",
									"type": "command",
									"command": "calva-fmt.formatCurrentForm"
								},
								{
									"key": "a",
									"name": "Align current form",
									"icon": "list-flat",
									"type": "command",
									"command": "calva-fmt.alignCurrentForm"
								},
								{
									"key": "d",
									"name": "Dedent line",
									"icon": "arrow-left",
									"type": "command",
									"command": "calva-fmt.tabDedent"
								},
								{
									"key": "i",
									"name": "Indent line",
									"icon": "arrow-right",
									"type": "command",
									"command": "calva-fmt.tabIndent"
								}
							]
						},
						{
							"key": "d",
							"name": "+Debug",
							"icon": "bug",
							"type": "bindings",
							"bindings": [
								{
									"key": "i",
									"name": "Last evaluation results",
									"icon": "chevron-right",
									"type": "command",
									"command": "calva.debug.instrument"
								},
								{
									"key": "r",
									"name": "Last evaluation results",
									"icon": "chevron-right",
									"type": "command",
									"command": "calva.copyLastResults"
								},
								{
									"key": "s",
									"name": "Last stacktrace",
									"icon": "debug-stackframe",
									"type": "command",
									"command": "calva.printLastStacktrace"
								}
							]
						},
						{
							"key": "e",
							"name": "+Evaluate",
							"icon": "chevron-right",
							"type": "bindings",
							"bindings": [
								{
									"key": ":",
									"name": "Evaluate current form as comment",
									"type": "command",
									"command": "calva.evaluateSelectionAsComment"
								},
								{
									"key": ";",
									"name": "Evaluate top-level form as comment",
									"type": "command",
									"command": "calva.evaluateTopLevelFormAsComment"
								},
								{
									"key": "e",
									"name": "Evaluate current expression",
									"type": "command",
									"command": "calva.evaluateSelection"
								},
								{
									"key": "f",
									"name": "Evaluate top-level expression",
									"type": "command",
									"command": "calva.evaluateCurrentTopLevelForm"
								},
								{
									"key": "i",
									"name": "Interrupt evaluation",
									"type": "command",
									"command": "calva.interruptAllEvaluations"
								},
								{
									"key": "l",
									"name": "Clear inline evaluation results",
									"type": "command",
									"command": "calva.clearInlineResults"
								},
								{
									"key": "n",
									"name": "Evaluate all code in namespace",
									"type": "command",
									"command": "calva.loadFile"
								},
								{
									"key": "s",
									"name": "Select expression",
									"type": "command",
									"command": "calva.selectCurrentForm"
								},
								{
									"key": "t",
									"name": "Clear evaluation results",
									"type": "command",
									"command": "calva.requireREPLUtilities"
								},
								{
									"key": "w",
									"name": "Replace form with evaluation result",
									"type": "command",
									"command": "calva.evaluateSelectionReplace"
								}
							]
						},
						{
							"key": "k",
							"name": "+Structural editing",
							"icon": "symbol-struct",
							"type": "bindings",
							"bindings": [
								{
									"key": ".",
									"name": "Toggle paredit mode",
									"type": "command",
									"command": "paredit.togglemode"
								},
								{
									"key": "b",
									"name": "Barf expression forward",
									"type": "command",
									"command": "paredit.barfSexpForward"
								},
								{
									"key": "c",
									"name": "Convolute expression",
									"type": "command",
									"command": "paredit.convolute"
								},
								{
									"key": "h",
									"name": "Backward expression",
									"type": "command",
									"command": "paredit.backwardSexp"
								},
								{
									"key": "j",
									"name": "Forward down expression",
									"type": "command",
									"command": "paredit.forwardDownSexp"
								},
								{
									"key": "k",
									"name": "Backward down expression",
									"type": "command",
									"command": "paredit.backwardDownSexp"
								},
								{
									"key": "l",
									"name": "Forward expression",
									"type": "command",
									"command": "paredit.forwardSexp"
								},
								{
									"key": "r",
									"name": "Raise expression",
									"type": "command",
									"command": "paredit.raiseSexp"
								},
								{
									"key": "s",
									"name": "Slurp expression forward",
									"type": "command",
									"command": "paredit.slurpSexpForward"
								},
								{
									"key": "t",
									"name": "Transpose expression",
									"type": "command",
									"command": "paredit.transpose"
								},
								{
									"key": "B",
									"name": "Barf expression backward",
									"type": "command",
									"command": "paredit.barfSexpBackward"
								},
								{
									"key": "H",
									"name": "Backward up expression",
									"type": "command",
									"command": "paredit.backwardUpSexp"
								},
								{
									"key": "J",
									"name": "Join expression",
									"type": "command",
									"command": "paredit.joinSexp"
								},
								{
									"key": "L",
									"name": "Forward up expression",
									"type": "command",
									"command": "paredit.forwardUpSexp"
								},
								{
									"key": "S",
									"name": "Slurp expression backward",
									"type": "command",
									"command": "paredit.slurpSexpBackward"
								},
								{
									"key": "w",
									"name": "+Wrap",
									"type": "bindings",
									"bindings": [
										{
											"key": "\"",
											"name": "Wrap around \"\"",
											"type": "command",
											"command": "paredit.wrapAroundQuote"
										},
										{
											"key": "(",
											"name": "Wrap around ()",
											"type": "command",
											"command": "paredit.wrapAroundParens"
										},
										{
											"key": "[",
											"name": "Wrap around []",
											"type": "command",
											"command": "paredit.wrapAroundSquare"
										},
										{
											"key": "c",
											"name": "Rewrap {}",
											"type": "command",
											"command": "paredit.rewrapCurly"
										},
										{
											"key": "p",
											"name": "Rewrap ()",
											"type": "command",
											"command": "paredit.rewrapParens"
										},
										{
											"key": "q",
											"name": "Rewrap \"\"",
											"type": "command",
											"command": "paredit.rewrapQuote"
										},
										{
											"key": "s",
											"name": "Rewrap []",
											"type": "command",
											"command": "paredit.rewrapSquare"
										},
										{
											"key": "{",
											"name": "Wrap around {}",
											"type": "command",
											"command": "paredit.wrapAroundCurly"
										}
									]
								}
							]
						},
						{
							"key": "m",
							"name": "+Manage REPL session",
							"icon": "repl",
							"type": "bindings",
							"bindings": [
								{
									"key": ".",
									"name": "Connect or jack-in",
									"type": "command",
									"command": "calva.jackInOrConnect"
								},
								{
									"key": "c",
									"name": "Connect to REPL server for project",
									"type": "command",
									"command": "calva.connect"
								},
								{
									"key": "j",
									"name": "Start REPL server for project (jack-in)",
									"type": "command",
									"command": "calva.jackIn"
								},
								{
									"key": "q",
									"name": "Disconnect (quit) from REPL server",
									"type": "command",
									"command": "calva.disconnect"
								},
								{
									"key": "r",
									"name": "Refresh changed namespaces",
									"type": "command",
									"command": "calva.refresh"
								},
								{
									"key": "s",
									"name": "Select cljs build connection",
									"type": "command",
									"command": "calva.switchCljsBuild"
								},
								{
									"key": "t",
									"name": "Toggle cljc session (clj, cljs)",
									"type": "command",
									"command": "calva.toggleCLJCSession"
								},
								{
									"key": "C",
									"name": "Run custom REPL command",
									"type": "command",
									"command": "calva.runCustomREPLCommand"
								},
								{
									"key": "R",
									"name": "Refresh all namespaces",
									"type": "command",
									"command": "calva.refreshAll"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "+Add",
									"type": "bindings",
									"bindings": [
										{
											"key": "l",
											"name": "Add missing library specification",
											"type": "command",
											"command": "calva.refactor.addMissingLibspec"
										}
									]
								},
								{
									"key": "c",
									"name": "+Cycle clean convert",
									"type": "bindings",
									"bindings": [
										{
											"key": "n",
											"name": "Clean namespace definition",
											"type": "command",
											"command": "calva.refactor.cleanNs"
										},
										{
											"key": "p",
											"name": "Cycle privacy",
											"type": "command",
											"command": "calva.refactor.cyclePrivacy"
										}
									]
								},
								{
									"key": "e",
									"name": "+Extract expand",
									"type": "bindings",
									"bindings": [
										{
											"key": "f",
											"name": "Extract function",
											"type": "command",
											"command": "calva.refactor.extractFunction"
										},
										{
											"key": "l",
											"name": "Expand let",
											"type": "command",
											"command": "calva.refactor.expandLet"
										}
									]
								},
								{
									"key": "i",
									"name": "+Introduce inline",
									"type": "bindings",
									"bindings": [
										{
											"key": "l",
											"name": "Introduce let",
											"type": "command",
											"command": "calva.refactor.introduceLet"
										},
										{
											"key": "s",
											"name": "Inline symbol",
											"type": "command",
											"command": "calva.refactor.inlineSymbol"
										}
									]
								},
								{
									"key": "m",
									"name": "+Move",
									"type": "bindings",
									"bindings": [
										{
											"key": "l",
											"name": "Move to let",
											"type": "command",
											"command": "calva.refactor.moveToLet"
										}
									]
								},
								{
									"key": "t",
									"name": "+Thread macros",
									"type": "bindings",
									"bindings": [
										{
											"key": "f",
											"name": "Thread first",
											"type": "command",
											"command": "calva.refactor.threadFirst"
										},
										{
											"key": "l",
											"name": "Thread last",
											"type": "command",
											"command": "calva.refactor.threadLast"
										},
										{
											"key": "u",
											"name": "Unwind thread",
											"type": "command",
											"command": "calva.refactor.unwindThread"
										},
										{
											"key": "F",
											"name": "Thread first all",
											"type": "command",
											"command": "calva.refactor.threadFirstAll"
										},
										{
											"key": "L",
											"name": "Thread last all",
											"type": "command",
											"command": "calva.refactor.threadLastAll"
										},
										{
											"key": "U",
											"name": "Unwind thread all",
											"type": "command",
											"command": "calva.refactor.unwindThread"
										}
									]
								}
							]
						},
						{
							"key": "t",
							"name": "+Tests",
							"icon": "beaker",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Run all tests",
									"icon": "beaker",
									"type": "command",
									"command": "calva.runAllTests"
								},
								{
									"key": "f",
									"name": "Run failing tests",
									"icon": "close",
									"type": "command",
									"command": "calva.rerunTests"
								},
								{
									"key": "n",
									"name": "Run tests in current namespace",
									"icon": "symbol-namespace",
									"type": "command",
									"command": "calva.runNamespaceTests"
								},
								{
									"key": "t",
									"name": "Run current test",
									"icon": "whole-word",
									"type": "command",
									"command": "calva.runTestUnderCursor"
								}
							]
						},
						{
							"key": "T",
							"name": "+Toggle",
							"icon": "settings",
							"type": "bindings",
							"bindings": [
								{
									"key": "p",
									"name": "Toggle pretty print results",
									"icon": "eye",
									"type": "command",
									"command": "calva.togglePrettyPrint"
								}
							]
						}
					]
				},
				{
					"key": "languageId:coq",
					"name": "coq",
					"type": "bindings",
					"bindings": [
						{
							"key": ".",
							"name": "Proof goto current point",
							"icon": "debug-start",
							"type": "command",
							"command": "extension.coq.interpretToPoint"
						},
						{
							"key": "b",
							"name": "Proof step back",
							"icon": "debug-step-back",
							"type": "command",
							"command": "extension.coq.stepBackward"
						},
						{
							"key": "f",
							"name": "Proof step forward",
							"icon": "debug-step-over",
							"type": "command",
							"command": "extension.coq.stepForward"
						},
						{
							"key": "g",
							"name": "Go to the current focus location",
							"icon": "sync",
							"type": "command",
							"command": "extension.coq.moveCursorToFocus"
						},
						{
							"key": "o",
							"name": "Open proof view",
							"icon": "open-preview",
							"type": "command",
							"command": "extension.coq.proofView.open"
						},
						{
							"key": "v",
							"name": "View the proof-state at the cursor position",
							"icon": "eye",
							"type": "command",
							"command": "extension.coq.proofView.viewStateAt"
						},
						{
							"key": "G",
							"name": "Proof goto end",
							"icon": "debug-continue",
							"type": "command",
							"command": "extension.coq.interpretToEnd"
						},
						{
							"key": "a",
							"name": "Ask prover",
							"icon": "question",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "About",
									"icon": "info",
									"type": "command",
									"command": "extension.coq.query.prompt.about"
								},
								{
									"key": "c",
									"name": "Check",
									"icon": "check",
									"type": "command",
									"command": "extension.coq.query.prompt.check"
								},
								{
									"key": "f",
									"name": "Find",
									"icon": "search",
									"type": "command",
									"command": "extension.coq.query.prompt.search"
								},
								{
									"key": "l",
									"name": "Locate",
									"icon": "location",
									"type": "command",
									"command": "extension.coq.query.prompt.locate"
								},
								{
									"key": "p",
									"name": "Print",
									"icon": "eye",
									"type": "command",
									"command": "extension.coq.query.prompt.print"
								}
							]
						},
						{
							"key": "p",
							"name": "Send command to prover",
							"icon": "console",
							"type": "bindings",
							"bindings": [
								{
									"key": "f",
									"name": "Finish coq computations",
									"icon": "notebook-state-success",
									"type": "command",
									"command": "extension.coq.finishComputations"
								},
								{
									"key": "i",
									"name": "Interrupt coqtop backend",
									"icon": "notebook-stop",
									"type": "command",
									"command": "extension.coq.interrupt"
								},
								{
									"key": "q",
									"name": "Quit coqtop backend",
									"icon": "panel-close",
									"type": "command",
									"command": "extension.coq.quit"
								},
								{
									"key": "r",
									"name": "Reset coqtop backend",
									"icon": "notebook-delete-cell",
									"type": "command",
									"command": "extension.coq.reset"
								}
							]
						},
						{
							"key": "q",
							"name": "Query prover about foucsed symbol",
							"icon": "info",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "About",
									"icon": "info",
									"type": "command",
									"command": "extension.coq.query.about"
								},
								{
									"key": "c",
									"name": "Check",
									"icon": "check",
									"type": "command",
									"command": "extension.coq.query.check"
								},
								{
									"key": "f",
									"name": "Find",
									"icon": "search",
									"type": "command",
									"command": "extension.coq.query.search"
								},
								{
									"key": "l",
									"name": "Locate",
									"icon": "location",
									"type": "command",
									"command": "extension.coq.query.locate"
								},
								{
									"key": "p",
									"name": "Print",
									"icon": "eye",
									"type": "command",
									"command": "extension.coq.query.print"
								}
							]
						},
						{
							"key": "T",
							"name": "UI toggle",
							"icon": "gear",
							"type": "bindings",
							"bindings": [
								{
									"key": "b",
									"name": "Toggle display of all basic low level contents",
									"icon": "symbol-interface",
									"type": "command",
									"command": "extension.coq.display.toggle.allBasicLowLevelContents"
								},
								{
									"key": "c",
									"name": "Toggle display of coercions",
									"icon": "symbol-enum",
									"type": "command",
									"command": "extension.coq.display.toggle.coercions"
								},
								{
									"key": "e",
									"name": "Toggle display of existential variable instances",
									"icon": "symbol-keyword",
									"type": "command",
									"command": "extension.coq.display.toggle.existentialVariableInstances"
								},
								{
									"key": "i",
									"name": "Toggle display of implicit arguments",
									"icon": "symbol-parameter",
									"type": "command",
									"command": "extension.coq.display.toggle.implicitArguments"
								},
								{
									"key": "l",
									"name": "Toggle display of all lowLevel contents",
									"type": "command",
									"icon": "symbol-constant",
									"command": "extension.coq.display.toggle.allLowLevelContents"
								},
								{
									"key": "n",
									"name": "Toggle display of notations",
									"icon": "symbol-key",
									"type": "command",
									"command": "extension.coq.display.toggle.notations"
								},
								{
									"key": "r",
									"name": "Toggle display of raw matching expressions",
									"icon": "symbol-constructor",
									"type": "command",
									"command": "extension.coq.display.toggle.rawMatchingExpressions"
								},
								{
									"key": "u",
									"name": "Toggle display of universe levels",
									"icon": "symbol-module",
									"type": "command",
									"command": "extension.coq.display.toggle.universeLevels"
								}
							]
						}
					]
				},
				{
					"key": "languageId:cpp",
					"name": "C++",
					"type": "bindings",
					"bindings": [
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "b",
							"name": "+Backend",
							"icon": "circuit-board",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Reset Database",
									"icon": "database",
									"type": "command",
									"command": "C_Cpp.ResetDatabase"
								},
								{
									"key": "w",
									"name": "Rescan Workspace",
									"icon": "project",
									"type": "command",
									"command": "C_Cpp.RescanWorkspace"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Switch Header/Source",
									"icon": "files",
									"type": "command",
									"command": "C_Cpp.SwitchHeaderSource"
								},
								{
									"key": "d",
									"name": "Go to declaration",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.revealDeclaration"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.actions.view.problems"
								},
								{
									"key": "f",
									"name": "Go to file in explorer",
									"icon": "file",
									"type": "command",
									"command": "workbench.files.action.showActiveFileInExplorer"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "r",
									"name": "Go to reference",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in buffer",
									"icon": "symbol-class",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "S",
									"name": "Go to symbol in project",
									"icon": "symbol-class",
									"type": "command",
									"command": "workbench.action.showAllSymbols"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": "r",
									"name": "Rename Symbol",
									"icon": "symbol-keyword",
									"type": "command",
									"command": "editor.action.rename"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek declaration",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.peekDeclaration"
								},
								{
									"key": "g",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								}
							]
						}
					]
				},
				{
					"key": "languageId:csharp",
					"name": "C#",
					"type": "bindings",
					"bindings": [
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "+Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "+Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "b",
							"name": "+Backend/OmniSharp",
							"icon": "circuit-board",
							"type": "bindings",
							"bindings": [
								{
									"key": "o",
									"name": "Show output",
									"icon": "output",
									"type": "command",
									"command": "o.showOutput"
								},
								{
									"key": "r",
									"name": "Restart OmniSharp",
									"icon": "server-process",
									"type": "command",
									"command": "o.restart"
								},
								{
									"key": "s",
									"name": "Select a project and start",
									"icon": "project",
									"type": "command",
									"command": "o.pickProjectAndStart"
								}
							]
						},
						{
							"key": "d",
							"name": "+Debug",
							"icon": "bug",
							"type": "bindings",
							"bindings": [
								{
									"key": "l",
									"name": "List process for attach",
									"icon": "server-process",
									"type": "command",
									"command": "csharp.listProcess"
								},
								{
									"key": "L",
									"name": "List remote processes for attach",
									"icon": "remote",
									"type": "command",
									"command": "csharp.listRemoteProcess"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.action.problems.focus"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "i",
									"name": "Go to implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.goToImplementation"
								},
								{
									"key": "r",
									"name": "Go to references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "I",
									"name": "Find implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "references-view.findImplementations"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								}
							]
						},
						{
							"key": "p",
							"name": "+Project",
							"icon": "project",
							"type": "bindings",
							"bindings": [
								{
									"key": "r",
									"name": "Restore project",
									"icon": "clock",
									"type": "command",
									"command": "dotnet.restore.project"
								},
								{
									"key": "R",
									"name": "Restore all projects",
									"icon": "clock",
									"type": "command",
									"command": "dotnet.restore.all"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": ".",
									"name": "Quick fix",
									"icon": "lightbulb-autofix",
									"type": "command",
									"command": "editor.action.quickFix"
								},
								{
									"key": "r",
									"name": "Rename symbol",
									"icon": "symbol-keyword",
									"type": "command",
									"command": "editor.action.rename"
								}
							]
						},
						{
							"key": "t",
							"name": "+Test",
							"icon": "beaker",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Debug test under cursor",
									"icon": "testing-debug-icon",
									"type": "command",
									"command": "dotnet.test.debugTestsInContext"
								},
								{
									"key": "t",
									"name": "Run test under cursor",
									"icon": "testing-run-icon",
									"type": "command",
									"command": "dotnet.test.runTestsInContext"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "i",
									"name": "Peek implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.peekImplementation"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								}
							]
						}
					]
				},
				{
					"key": "languageId:dart",
					"name": "Dart/Flutter",
					"type": "bindings",
					"bindings": [
						{
							"key": ";",
							"name": "Toggle Dartdoc comment",
							"icon": "comment",
							"type": "command",
							"command": "dart.toggleDartdocComment"
						},
						{
							"key": "a",
							"name": "Attach",
							"icon": "remote-explorer",
							"type": "command",
							"command": "flutter.attach"
						},
						{
							"key": "c",
							"name": "Clean",
							"icon": "trash",
							"type": "command",
							"command": "flutter.clean"
						},
						{
							"key": "i",
							"name": "Inspect widget",
							"icon": "telescope",
							"type": "command",
							"command": "flutter.inspectWidget"
						},
						{
							"key": "m",
							"name": "Sort members",
							"icon": "selection",
							"type": "command",
							"command": "dart.sortMembers"
						},
						{
							"key": "r",
							"name": "Hot reload",
							"icon": "zap",
							"type": "command",
							"command": "flutter.hotReload"
						},
						{
							"key": "s",
							"name": "Select device",
							"icon": "vm-active",
							"type": "command",
							"command": "flutter.selectDevice"
						},
						{
							"key": "u",
							"name": "Flutter upgrade",
							"icon": "cloud-upload",
							"type": "command",
							"command": "flutter.upgrade"
						},
						{
							"key": "A",
							"name": "Attach to process",
							"icon": "server-process",
							"type": "command",
							"command": "flutter.attachProcess"
						},
						{
							"key": "D",
							"name": "Flutter doctor",
							"icon": "hubot",
							"type": "command",
							"command": "flutter.doctor"
						},
						{
							"key": "E",
							"name": "Launch emulator",
							"icon": "rocket",
							"type": "command",
							"command": "flutter.launchEmulator"
						},
						{
							"key": "P",
							"name": "Profile app",
							"icon": "search",
							"type": "command",
							"command": "flutter.profileApp"
						},
						{
							"key": "R",
							"name": "Hot restart",
							"icon": "sync",
							"type": "command",
							"command": "flutter.hotRestart"
						},
						{
							"key": "S",
							"name": "Screenshot",
							"icon": "device-camera",
							"type": "command",
							"command": "flutter.screenshot"
						},
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "+Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "+Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.action.problems.focus"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "i",
									"name": "Go to implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.goToImplementation"
								},
								{
									"key": "r",
									"name": "Go to references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to super",
									"icon": "symbol-class",
									"type": "command",
									"command": "dart.goToSuper"
								},
								{
									"key": "t",
									"name": "Go to test/implementation file",
									"icon": "beaker",
									"type": "command",
									"command": "dart.goToTestOrImplementationFile"
								},
								{
									"key": "I",
									"name": "Find implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "references-view.findImplementations"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "T",
									"name": "Go to tests",
									"icon": "list-tree",
									"type": "command",
									"command": "dart.goToTests"
								}
							]
						},
						{
							"key": "l",
							"name": "+Logging",
							"icon": "output",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Start logging analysis server",
									"icon": "server-process",
									"type": "command",
									"command": "dart.startLoggingAnalysisServer"
								},
								{
									"key": "d",
									"name": "Start logging debugging",
									"icon": "bug",
									"type": "command",
									"command": "dart.startLoggingDebugging"
								},
								{
									"key": "e",
									"name": "Start logging extension only",
									"icon": "output",
									"type": "command",
									"command": "dart.startLoggingExtensionOnly"
								},
								{
									"key": "s",
									"name": "Start logging",
									"icon": "output",
									"type": "command",
									"command": "dart.startLogging"
								},
								{
									"key": "S",
									"name": "Stop logging",
									"icon": "output",
									"type": "command",
									"command": "dart.stopLogging"
								}
							]
						},
						{
							"key": "o",
							"name": "+Open",
							"icon": "folder-opened",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Analyzer diagnostics",
									"icon": "output",
									"type": "command",
									"command": "dart.openAnalyzerDiagnostics"
								},
								{
									"key": "c",
									"name": "DevTools CPU profiler",
									"icon": "telescope",
									"type": "command",
									"command": "dart.startLoggingDebugging"
								},
								{
									"key": "d",
									"name": "Devtools",
									"icon": "tools",
									"type": "command",
									"command": "flutter.openDevTools"
								},
								{
									"key": "l",
									"name": "DevTools logging",
									"icon": "output",
									"type": "command",
									"command": "dart.openDevToolsLogging"
								},
								{
									"key": "m",
									"name": "DevTools memory",
									"icon": "files",
									"type": "command",
									"command": "dart.openDevToolsMemory"
								},
								{
									"key": "n",
									"name": "DevTools network",
									"icon": "pulse",
									"type": "command",
									"command": "dart.openDevToolsNetwork"
								},
								{
									"key": "t",
									"name": "Timeline",
									"icon": "clock",
									"type": "command",
									"command": "flutter.openTimeline"
								}
							]
						},
						{
							"key": "p",
							"name": "+Project/Packages",
							"icon": "project",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Add dependency",
									"icon": "symbol-module",
									"type": "command",
									"command": "dart.addDependency"
								},
								{
									"key": "g",
									"name": "Pub get",
									"icon": "cloud-download",
									"type": "command",
									"command": "flutter.packages.get"
								},
								{
									"key": "o",
									"name": "Pub outdated",
									"icon": "compare-changes",
									"type": "command",
									"command": "flutter.packages.outdated"
								},
								{
									"key": "u",
									"name": "Pub upgrade",
									"icon": "cloud-upload",
									"type": "command",
									"command": "flutter.packages.upgrade"
								},
								{
									"key": "D",
									"name": "Add dev dependency",
									"icon": "symbol-module",
									"type": "command",
									"command": "dart.addDevDependency"
								},
								{
									"key": "U",
									"name": "Pub upgrade -major versions",
									"icon": "cloud-upload",
									"type": "command",
									"command": "flutter.packages.upgrade.majorVersions"
								},
								{
									"key": "c",
									"name": "+Create",
									"icon": "add",
									"type": "bindings",
									"bindings": [
										{
											"key": "d",
											"name": "Dart project",
											"icon": "rocket",
											"type": "command",
											"commmand": "dart.createProject"
										},
										{
											"key": "l",
											"name": "Flutter plugin project",
											"icon": "plug",
											"type": "command",
											"commmand": "flutter.createProject.plugin"
										},
										{
											"key": "m",
											"name": "Flutter module project",
											"icon": "module",
											"type": "command",
											"commmand": "flutter.createProject.module"
										},
										{
											"key": "p",
											"name": "Flutter project",
											"icon": "project",
											"type": "command",
											"commmand": "flutter.createProject"
										},
										{
											"key": "D",
											"name": "Create DartDoc",
											"icon": "book",
											"type": "command",
											"commmand": "dart.task.dartdoc"
										},
										{
											"key": "P",
											"name": "Flutter package project",
											"icon": "package",
											"type": "command",
											"commmand": "flutter.createProject.package"
										}
									]
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": ".",
									"name": "Quick fix",
									"icon": "lightbulb-autofix",
									"type": "command",
									"command": "editor.action.quickFix"
								},
								{
									"key": "r",
									"name": "Rename symbol",
									"icon": "symbol-keyword",
									"type": "command",
									"command": "editor.action.rename"
								}
							]
						},
						{
							"key": "t",
							"name": "+Test",
							"icon": "beaker",
							"type": "bindings",
							"bindings": [
								{
									"key": "c",
									"name": "Clear test results",
									"icon": "trash",
									"type": "command",
									"command": "dart.clearTestResults"
								},
								{
									"key": "d",
									"name": "Debug test at cursor",
									"icon": "testing-debug-icon",
									"type": "command",
									"command": "dart.debugTestAtCursor"
								},
								{
									"key": "f",
									"name": "Run failed tests",
									"icon": "testing-failed-icon",
									"type": "command",
									"command": "dart.runAllFailedTestsWithoutDebugging"
								},
								{
									"key": "r",
									"name": "Run tests",
									"icon": "run-all",
									"type": "command",
									"command": "dart.runAllTestsWithoutDebugging"
								},
								{
									"key": "s",
									"name": "Run skipped tests",
									"icon": "debug-step-over",
									"type": "command",
									"command": "dart.runAllTestsWithoutDebugging"
								},
								{
									"key": "t",
									"name": "Run test at cursor",
									"icon": "testing-run-icon",
									"type": "command",
									"command": "dart.runTestAtCursor"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "i",
									"name": "Peek implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.peekImplementation"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								}
							]
						},
						{
							"key": "T",
							"name": "+Toggle",
							"icon": "settings",
							"type": "bindings",
							"bindings": [
								{
									"key": "b",
									"name": "Brightness",
									"icon": "star-half",
									"type": "command",
									"command": "flutter.toggleBrightness"
								},
								{
									"key": "d",
									"name": "Debug painting",
									"icon": "paintcan",
									"type": "command",
									"command": "flutter.toggleDebugPainting"
								},
								{
									"key": "e",
									"name": "Check elevations",
									"icon": "check",
									"type": "command",
									"command": "flutter.toggleCheckElevations"
								},
								{
									"key": "o",
									"name": "Performance overlay",
									"icon": "output",
									"type": "command",
									"command": "flutter.togglePerformanceOverlay"
								},
								{
									"key": "p",
									"name": "Paint baselines",
									"icon": "paintcan",
									"type": "command",
									"command": "flutter.togglePaintBaselines"
								},
								{
									"key": "r",
									"name": "Repaint rainbow",
									"icon": "symbol-color",
									"type": "command",
									"command": "flutter.toggleRepaintRainbow"
								},
								{
									"key": "s",
									"name": "Slow animations",
									"icon": "clock",
									"type": "command",
									"command": "flutter.toggleSlowAnimations"
								},
								{
									"key": "B",
									"name": "Debug mode banner",
									"icon": "bug",
									"type": "command",
									"command": "flutter.toggleDebugModeBanner"
								}
							]
						}
					]
				},
				{
					"key": "languageId:elixir",
					"name": "Elixir",
					"type": "bindings",
					"bindings": [
						{
							"key": "o",
							"name": "Expand selected macro",
							"icon": "symbol-function",
							"type": "command",
							"command": "extension.expandMacro"
						},
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "+Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "+Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.action.problems.focus"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "i",
									"name": "Go to implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.goToImplementation"
								},
								{
									"key": "r",
									"name": "Go to references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "I",
									"name": "Find implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "references-view.findImplementations"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": ".",
									"name": "Quick fix",
									"icon": "lightbulb-autofix",
									"type": "command",
									"command": "editor.action.quickFix"
								},
								{
									"key": "p",
									"name": "Transform function call to pipe operator",
									"icon": "lightbulb-autofix",
									"type": "command",
									"command": "extension.toPipe"
								},
								{
									"key": "r",
									"name": "Rename symbol",
									"icon": "symbol-keyword",
									"type": "command",
									"command": "editor.action.rename"
								},
								{
									"key": "P",
									"name": "Transform pipe operator to function call",
									"icon": "lightbulb-autofix",
									"type": "command",
									"command": "extension.fromPipe"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "i",
									"name": "Peek implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.peekImplementation"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								}
							]
						}
					]
				},
				{
					"key": "languageId:fsharp",
					"name": "F#",
					"type": "bindings",
					"bindings": [
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "+Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "+Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "c",
							"name": "+Compile",
							"icon": "gear",
							"type": "bindings",
							"bindings": [
								{
									"key": "c",
									"name": "MSBuild: Build current solution",
									"icon": "package",
									"type": "command",
									"command": "MSBuild.buildCurrentSolution"
								},
								{
									"key": "d",
									"name": "F#: Run default project",
									"icon": "play",
									"type": "command",
									"command": "fsharp.runDefaultProject"
								},
								{
									"key": "l",
									"name": "MSBuild: Clean current solution",
									"icon": "trash",
									"type": "command",
									"command": "MSBuild.cleanCurrentSolution"
								},
								{
									"key": "p",
									"name": "MSBuild: Build current project",
									"icon": "project",
									"type": "command",
									"command": "MSBuild.buildCurrent"
								},
								{
									"key": "r",
									"name": "MSBuild: Re-build current solution",
									"icon": "refresh",
									"type": "command",
									"command": "MSBuild.rebuildCurrentSolution"
								},
								{
									"key": "D",
									"name": "F#: Debug default project",
									"icon": "bug",
									"type": "command",
									"command": "fsharp.debugDefaultProject"
								},
								{
									"key": "L",
									"name": "MSBuild: Clean current project",
									"icon": "trash",
									"type": "command",
									"command": "MSBuild.cleanCurrent"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.action.problems.focus"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "r",
									"name": "Go to reference",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in buffer",
									"icon": "file",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "t",
									"name": "Go to type definition",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.goToTypeDefinition"
								},
								{
									"key": "I",
									"name": "Find implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "references-view.findImplementations"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": "r",
									"name": "Rename symbol",
									"icon": "symbol-keyword",
									"type": "command",
									"command": "editor.action.rename"
								}
							]
						},
						{
							"key": "s",
							"name": "+FSI REPL",
							"icon": "repl",
							"type": "bindings",
							"bindings": [
								{
									"key": "f",
									"name": "FSI: Send file",
									"icon": "file",
									"type": "command",
									"command": "fsi.SendFile"
								},
								{
									"key": "l",
									"name": "FSI: Send line",
									"type": "command",
									"icon": "list-flat",
									"command": "fsi.SendLine"
								},
								{
									"key": "s",
									"name": "FSI: Send selection",
									"icon": "list-selection",
									"type": "command",
									"command": "fsi.SendSelection"
								},
								{
									"key": "G",
									"name": "FSI: Generate project references",
									"icon": "references",
									"type": "command",
									"command": "fsi.GenerateProjectReferences"
								},
								{
									"key": "L",
									"name": "FSI: Send last selection",
									"icon": "list-selection",
									"type": "command",
									"command": "fsi.SendLastSelection"
								},
								{
									"key": "P",
									"name": "FSI: Send references from project",
									"icon": "project",
									"type": "command",
									"command": "fsi.SendProjectReferences"
								},
								{
									"key": "S",
									"name": "FSI: Start",
									"icon": "repl",
									"type": "command",
									"command": "fsi.Start"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								},
								{
									"key": "t",
									"name": "Peek type definition",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.peekTypeDefinition"
								}
							]
						}
					]
				},
				{
					"key": "languageId:go",
					"name": "Go",
					"type": "bindings",
					"bindings": [
						{
							"key": " ",
							"name": "Show all commands",
							"icon": "rocket",
							"type": "command",
							"command": "go.show.commands"
						},
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "+Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "+Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "a",
							"name": "+Actions",
							"icon": "zap",
							"type": "bindings",
							"bindings": [
								{
									"key": "P",
									"name": "Run code on Go Playground",
									"icon": "squirrel",
									"type": "command",
									"command": "go.playground"
								},
								{
									"key": "p",
									"name": "+Package actions",
									"icon": "package",
									"type": "bindings",
									"bindings": [
										{
											"key": "b",
											"name": "Build package",
											"icon": "gear",
											"type": "command",
											"command": "go.build.package"
										},
										{
											"key": "g",
											"name": "Get package",
											"icon": "cloud-download",
											"type": "command",
											"command": "go.get.package"
										},
										{
											"key": "i",
											"name": "Install current package",
											"icon": "package",
											"type": "command",
											"command": "go.install.package"
										},
										{
											"key": "l",
											"name": "Lint package",
											"icon": "warning",
											"type": "command",
											"command": "go.lint.package"
										},
										{
											"key": "s",
											"name": "Browse packages",
											"icon": "search",
											"type": "command",
											"command": "go.browse.packages"
										},
										{
											"key": "v",
											"name": "Vet package",
											"icon": "dashboard",
											"type": "command",
											"command": "go.vet.package"
										}
									]
								},
								{
									"key": "w",
									"name": "+Workspace actions",
									"icon": "project",
									"type": "bindings",
									"bindings": [
										{
											"key": "b",
											"name": "Build workspace",
											"icon": "gear",
											"type": "command",
											"command": "go.build.workspace"
										},
										{
											"key": "l",
											"name": "Lint workspace",
											"icon": "warning",
											"type": "command",
											"command": "go.lint.workspace"
										},
										{
											"key": "p",
											"name": "Add package to workspace",
											"icon": "add",
											"type": "command",
											"command": "go.add.package.workspace"
										},
										{
											"key": "v",
											"name": "Vet workspace",
											"icon": "dashboard",
											"type": "command",
											"command": "go.vet.workspace"
										}
									]
								}
							]
						},
						{
							"key": "b",
							"name": "+Backend/environment",
							"icon": "circuit-board",
							"type": "bindings",
							"bindings": [
								{
									"key": "e",
									"name": "Choose Go environment",
									"icon": "package",
									"type": "command",
									"command": "go.environment.choose"
								},
								{
									"key": "g",
									"name": "Show current GOPATH",
									"icon": "file-submodule",
									"type": "command",
									"command": "go.gopath"
								},
								{
									"key": "i",
									"name": "Install/update tools",
									"icon": "cloud-download",
									"type": "command",
									"command": "go.tools.install"
								},
								{
									"key": "l",
									"name": "Locate configured Go tools",
									"icon": "tools",
									"type": "command",
									"command": "go.locate.tools"
								},
								{
									"key": "R",
									"name": "Restart language server",
									"icon": "server-process",
									"type": "command",
									"command": "go.languageserver.restart"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.action.problems.focus"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "h",
									"name": "Show call hierarchy",
									"icon": "type-hierarchy",
									"type": "command",
									"command": "references-view.showCallHierarchy"
								},
								{
									"key": "i",
									"name": "Go to implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.goToImplementation"
								},
								{
									"key": "r",
									"name": "Go to references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "t",
									"name": "Go to type definition",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.goToTypeDefinition"
								},
								{
									"key": "I",
									"name": "Find implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "references-view.findImplementations"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								}
							]
						},
						{
							"key": "i",
							"name": "+Insert/remove",
							"icon": "add",
							"type": "bindings",
							"bindings": [
								{
									"key": "f",
									"name": "Fill struct",
									"icon": "symbol-struct",
									"type": "command",
									"command": "go.fill.struct"
								},
								{
									"key": "i",
									"name": "Add import",
									"icon": "symbol-reference",
									"type": "command",
									"command": "go.import.add"
								},
								{
									"key": "t",
									"name": "Add tags to struct fields",
									"icon": "add",
									"type": "command",
									"command": "go.add.tags"
								},
								{
									"key": "I",
									"name": "Generate interface stubs",
									"icon": "symbol-interface",
									"type": "command",
									"command": "go.impl.cursor"
								},
								{
									"key": "T",
									"name": "Remove tags from struct fields",
									"icon": "remove",
									"type": "command",
									"command": "go.remove.tags"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": ".",
									"name": "Quick fix",
									"icon": "lightbulb-autofix",
									"type": "command",
									"command": "editor.action.quickFix"
								},
								{
									"key": "e",
									"name": "Extract to function or variable",
									"icon": "gather",
									"type": "command",
									"command": "editor.action.codeAction",
									"args": {
										"kind": "refactor.extract"
									}
								},
								{
									"key": "r",
									"name": "Rename symbol",
									"icon": "symbol-keyword",
									"type": "command",
									"command": "editor.action.rename"
								}
							]
						},
						{
							"key": "t",
							"name": "+Test",
							"icon": "beaker",
							"type": "bindings",
							"bindings": [
								{
									"key": "c",
									"name": "Cancel running tests",
									"icon": "close",
									"type": "command",
									"command": "go.test.cancel"
								},
								{
									"key": "d",
									"name": "Debug test at cursor",
									"icon": "bug",
									"type": "command",
									"command": "go.debug.cursor"
								},
								{
									"key": "f",
									"name": "Test file",
									"icon": "file",
									"type": "command",
									"command": "go.test.file"
								},
								{
									"key": "l",
									"name": "Test previous",
									"icon": "clock",
									"type": "command",
									"command": "go.test.previous"
								},
								{
									"key": "p",
									"name": "Test package",
									"icon": "package",
									"type": "command",
									"command": "go.test.package"
								},
								{
									"key": "s",
									"name": "Subtest at cursor",
									"icon": "whole-word",
									"type": "command",
									"command": "go.subtest.cursor"
								},
								{
									"key": "t",
									"name": "Test function at cursor",
									"icon": "whole-word",
									"type": "command",
									"command": "go.test.cursor"
								},
								{
									"key": "w",
									"name": "Test packages in workspace",
									"icon": "project",
									"type": "command",
									"command": "go.test.workspace"
								},
								{
									"key": "P",
									"name": "Apply cover profile",
									"icon": "jersey",
									"type": "command",
									"command": "go.apply.coverprofile"
								},
								{
									"key": "b",
									"name": "+Benchmarks",
									"icon": "dashboard",
									"type": "bindings",
									"bindings": [
										{
											"key": "f",
											"name": "Benchmark function at cursor",
											"icon": "whole-word",
											"type": "command",
											"command": "go.benchmark.cursor"
										},
										{
											"key": "p",
											"name": "Benchmark package",
											"icon": "package",
											"type": "command",
											"command": "go.benchmark.package"
										},
										{
											"key": "F",
											"name": "Benchmark file",
											"icon": "file",
											"type": "command",
											"command": "go.benchmark.file"
										}
									]
								},
								{
									"key": "g",
									"name": "+Generate",
									"icon": "gear",
									"type": "bindings",
									"bindings": [
										{
											"key": "f",
											"name": "Generate unit tests for function",
											"icon": "symbol-function",
											"type": "command",
											"command": "go.test.generate.function"
										},
										{
											"key": "p",
											"name": "Generate unit tests for package",
											"icon": "package",
											"type": "command",
											"command": "go.test.generate.package"
										},
										{
											"key": "F",
											"name": "Generate unit tests for file",
											"icon": "file",
											"type": "command",
											"command": "go.test.generate.file"
										}
									]
								},
								{
									"key": "T",
									"name": "+Toggle",
									"icon": "settings",
									"type": "bindings",
									"bindings": [
										{
											"key": "c",
											"name": "Toggle test coverage in current package",
											"icon": "package",
											"type": "command",
											"command": "go.test.coverage"
										},
										{
											"key": "f",
											"name": "Toggle open test file",
											"icon": "file",
											"type": "command",
											"command": "go.toggle.test.file"
										}
									]
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "h",
									"name": "Peek call hierarchy",
									"icon": "type-hierarchy",
									"type": "command",
									"command": "editor.showCallHierarchy"
								},
								{
									"key": "i",
									"name": "Peek implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.peekImplementation"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								}
							]
						}
					]
				},
				{
					"key": "languageId:java",
					"name": "Java",
					"type": "bindings",
					"bindings": [
						{
							"key": "h",
							"name": "Describe thing at point",
							"icon": "book",
							"type": "command",
							"command": "editor.action.showHover"
						},
						{
							"key": "D",
							"name": "Debug Java file",
							"icon": "debug-alt",
							"type": "command",
							"command": "java.debug.debugJavaFile"
						},
						{
							"key": "R",
							"name": "Run Java file",
							"icon": "run",
							"type": "command",
							"command": "java.debug.runJavaFile"
						},
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "a",
							"name": "+Code actions",
							"icon": "zap",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Execute code action",
									"icon": "lightbulb",
									"type": "command",
									"command": "editor.action.codeAction"
								},
								{
									"key": "f",
									"name": "Execute fix action",
									"icon": "lightbulb-autofix",
									"type": "command",
									"command": "editor.action.quickFix"
								},
								{
									"key": "r",
									"name": "Refactor action",
									"icon": "edit",
									"type": "command",
									"command": "editor.action.refactor"
								},
								{
									"key": "s",
									"name": "Source action",
									"icon": "lightbulb",
									"type": "command",
									"command": "editor.action.sourceAction"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "e",
									"name": "Go to error list",
									"icon": "command",
									"type": "command",
									"command": "workbench.action.showErrorsWarnings"
								},
								{
									"key": "h",
									"name": "Show call hierarchy",
									"icon": "type-hierarchy",
									"type": "command",
									"command": "references-view.showCallHierarchy"
								},
								{
									"key": "i",
									"name": "Go to implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.goToImplementation"
								},
								{
									"key": "o",
									"name": "Go to super implementation",
									"icon": "symbol-module",
									"type": "command",
									"command": "java.action.navigateToSuperImplementation"
								},
								{
									"key": "r",
									"name": "Go to references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in buffer",
									"icon": "file",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "t",
									"name": "Go to type definition",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.goToTypeDefinition"
								},
								{
									"key": "u",
									"name": "Go to subtype hierarchy",
									"icon": "type-hierarchy",
									"type": "command",
									"command": "java.action.showSubtypeHierarchy"
								},
								{
									"key": "H",
									"name": "Go to type hierarchy",
									"icon": "type-hierarchy",
									"type": "command",
									"command": "java.action.showTypeHierarchy"
								},
								{
									"key": "I",
									"name": "Find implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "references-view.findImplementations"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "S",
									"name": "Go to symbol in project",
									"icon": "project",
									"type": "command",
									"command": "workbench.action.showAllSymbols"
								},
								{
									"key": "T",
									"name": "Go to test",
									"icon": "beaker",
									"type": "command",
									"command": "java.test.goToTest"
								},
								{
									"key": "U",
									"name": "Go to supertype hierarchy",
									"icon": "type-hierarchy",
									"type": "command",
									"command": "java.action.showSupertypeHierarchy"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Execute code actions",
									"icon": "lightbulb",
									"type": "command",
									"command": "editor.action.codeAction"
								},
								{
									"key": "e",
									"name": "Extract to function or variable",
									"icon": "gather",
									"type": "command",
									"command": "editor.action.codeAction",
									"args": {
										"kind": "refactor.extract"
									}
								},
								{
									"key": "o",
									"name": "Organize imports",
									"icon": "edit",
									"type": "command",
									"command": "editor.action.organizeImports"
								},
								{
									"key": "r",
									"name": "Rename symbol",
									"icon": "edit",
									"type": "command",
									"command": "editor.action.rename"
								},
								{
									"key": "R",
									"name": "Refactor actions",
									"icon": "edit",
									"type": "command",
									"command": "editor.action.refactor"
								}
							]
						},
						{
							"key": "t",
							"name": "+Test",
							"icon": "beaker",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Run all tests",
									"icon": "beaker",
									"type": "command",
									"command": "testing.runAll"
								},
								{
									"key": "b",
									"name": "Run current test file",
									"icon": "file",
									"type": "command",
									"command": "testing.runCurrentFile"
								},
								{
									"key": "r",
									"name": "Re-run failed tests",
									"icon": "close",
									"type": "command",
									"command": "testing.reRunFailTests"
								},
								{
									"key": "t",
									"name": "Select and run test",
									"icon": "list-unordered",
									"type": "command",
									"command": "testing.runSelected"
								},
								{
									"key": "A",
									"name": "Debug all tests",
									"icon": "bug",
									"type": "command",
									"command": "testing.debugAll"
								},
								{
									"key": "T",
									"name": "Select and debug test",
									"icon": "debug-alt",
									"type": "command",
									"command": "testing.debugSelected"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "h",
									"name": "Peek call hierarchy",
									"icon": "type-hierarchy",
									"type": "command",
									"command": "editor.showCallHierarchy"
								},
								{
									"key": "i",
									"name": "Peek implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.peekImplementation"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								},
								{
									"key": "t",
									"name": "Peek type definition",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.peekTypeDefinition"
								}
							]
						}
					]
				},
				{
					"key": "languageId:javascript",
					"name": "JavaScript",
					"type": "bindings",
					"bindings": [
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "+Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "+Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "h",
									"name": "Show call hierarchy",
									"icon": "type-hierarchy",
									"type": "command",
									"command": "references-view.showCallHierarchy"
								},
								{
									"key": "r",
									"name": "Go to reference",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in buffer",
									"icon": "file",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "t",
									"name": "Go to type definition",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.goToTypeDefinition"
								},
								{
									"key": "I",
									"name": "Find implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "references-view.findImplementations"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "S",
									"name": "Go to symbol in project",
									"icon": "project",
									"type": "command",
									"command": "workbench.action.showAllSymbols"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "h",
									"name": "Peek call hierarchy",
									"icon": "type-hierarchy",
									"type": "command",
									"command": "editor.showCallHierarchy"
								},
								{
									"key": "i",
									"name": "Peek implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.peekImplementation"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								},
								{
									"key": "t",
									"name": "Peek type definition",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.peekTypeDefinition"
								}
							]
						}
					]
				},
				{
					"key": "languageId:julia",
					"name": "Julia",
					"type": "bindings",
					"bindings": [
						{
							"key": ",",
							"name": "Execute code in REPL",
							"icon": "play",
							"type": "command",
							"command": "language-julia.executeJuliaCodeInREPL"
						},
						{
							"key": "d",
							"name": "Show documentation",
							"icon": "book",
							"type": "command",
							"command": "language-julia.show-documentation"
						},
						{
							"key": "p",
							"name": "Show plots",
							"icon": "pulse",
							"type": "command",
							"command": "language-julia.show-plotpane"
						},
						{
							"key": "w",
							"name": "Focus on workspace view",
							"icon": "play",
							"type": "command",
							"command": "REPLVariables.focus"
						},
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "+Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "+Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "b",
							"name": "+Backend",
							"icon": "circuit-board",
							"type": "bindings",
							"bindings": [
								{
									"key": "i",
									"name": "Re-index language server cache",
									"icon": "output",
									"type": "command",
									"command": "language-julia.refreshLanguageServer"
								},
								{
									"key": "l",
									"name": "Toggle linter",
									"icon": "check",
									"type": "command",
									"command": "language-julia.toggleLinter"
								},
								{
									"key": "r",
									"name": "Restart language server",
									"icon": "server-process",
									"type": "command",
									"command": "language-julia.restartLanguageServer"
								}
							]
						},
						{
							"key": "c",
							"name": "+Compile/debug",
							"icon": "play",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Add to compiled modules/functions",
									"icon": "plus",
									"type": "command",
									"command": "language-julia.switchToCompiled"
								},
								{
									"key": "c",
									"name": "Switch all to compiled",
									"icon": "debug",
									"type": "command",
									"command": "language-julia.switchAllToCompiled"
								},
								{
									"key": "d",
									"name": "Debug file in new process",
									"icon": "debug-alt",
									"type": "command",
									"command": "language-julia.debugEditorContents"
								},
								{
									"key": "i",
									"name": "Switch all to interpreted",
									"icon": "run-below",
									"type": "command",
									"command": "language-julia.switchAllToInterpreted"
								},
								{
									"key": "m",
									"name": "Enable compiled mode for the debugger",
									"icon": "debug-breakpoint-log",
									"type": "command",
									"command": "language-julia.enable-compiled-mode"
								},
								{
									"key": "r",
									"name": "Refresh compiled/interpreted pane",
									"icon": "refresh",
									"type": "command",
									"command": "language-julia.refreshCompiled"
								},
								{
									"key": "x",
									"name": "Remove from compiled modules/functions",
									"icon": "diff-removed",
									"type": "command",
									"command": "language-julia.switchToInterpreted"
								},
								{
									"key": "A",
									"name": "Apply default compiled modules/functions",
									"icon": "diff-renamed",
									"type": "command",
									"command": "language-julia.apply-compiled-defaults"
								},
								{
									"key": "D",
									"name": "Clear compiled modules/functions",
									"icon": "diff-removed",
									"type": "command",
									"command": "language-julia.reset-compiled"
								},
								{
									"key": "F",
									"name": "Set current compiled modules/functions as default",
									"icon": "symbol-constant",
									"type": "command",
									"command": "language-julia.set-current-as-default-compiled"
								},
								{
									"key": "M",
									"name": "Disable compiled mode for the debugger",
									"icon": "debug-breakpoint-unverified",
									"type": "command",
									"command": "language-julia.disable-compiled-mode"
								},
								{
									"key": "R",
									"name": "Restart kernel",
									"icon": "debug-restart",
									"type": "command",
									"command": "language-julia.restartKernel"
								},
								{
									"key": "S",
									"name": "Stop kernel",
									"icon": "debug-stop",
									"type": "command",
									"command": "language-julia.stopKernel"
								},
								{
									"key": "Y",
									"name": "Add symbol to compiled modules/functions",
									"icon": "symbol-key",
									"type": "command",
									"command": "language-julia.set-compiled-for-name"
								}
							]
						},
						{
							"key": "c",
							"name": "+Clear",
							"icon": "trash",
							"type": "bindings",
							"bindings": [
								{
									"key": "c",
									"name": "Clear current inline results",
									"icon": "chrome-close",
									"type": "command",
									"command": "language-julia.clearCurrentInlineResult"
								},
								{
									"key": "C",
									"name": "Clear all inline results",
									"icon": "clear-all",
									"type": "command",
									"command": "language-julia.clearAllInlineResults"
								},
								{
									"key": "K",
									"name": "Clear all inline results in editor",
									"icon": "clear-all",
									"type": "command",
									"command": "language-julia.clearAllInlineResultsInEditor"
								}
							]
						},
						{
							"key": "e",
							"name": "+Environment/package",
							"icon": "library",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Activate this environment",
									"icon": "check",
									"type": "command",
									"command": "language-julia.changeCurrentEnvironment"
								},
								{
									"key": "c",
									"name": "Change current environment",
									"icon": "issue-reopened",
									"type": "command",
									"command": "language-julia.changeCurrentEnvironment"
								},
								{
									"key": "m",
									"name": "Choose module",
									"icon": "symbol-variable",
									"type": "command",
									"command": "language-julia.chooseModule"
								},
								{
									"key": "p",
									"name": "Activate parent environment",
									"icon": "root-folder-opened",
									"type": "command",
									"command": "language-julia.changeCurrentEnvironment"
								},
								{
									"key": "t",
									"name": "Tag new package version",
									"icon": "tag",
									"type": "command",
									"command": "language-julia.tagNewPackageVersion"
								},
								{
									"key": "P",
									"name": "Open package directory",
									"icon": "new-folder",
									"type": "command",
									"command": "language-julia.openPackageDirectory"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.action.problems.focus"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "r",
									"name": "Go to references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in buffer",
									"icon": "file",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "S",
									"name": "Go to symbol in project",
									"icon": "project",
									"type": "command",
									"command": "workbench.action.showAllSymbols"
								}
							]
						},
						{
							"key": "s",
							"name": "+Send/REPL",
							"icon": "repl",
							"type": "bindings",
							"bindings": [
								{
									"key": "b",
									"name": "Execute block or selection in REPL",
									"icon": "selection",
									"type": "command",
									"command": "language-julia.executeCodeBlockOrSelection"
								},
								{
									"key": "c",
									"name": "Execute code cell in REPL and move",
									"icon": "export",
									"type": "command",
									"command": "language-julia.executeCellAndMove"
								},
								{
									"key": "d",
									"name": "Change directory here",
									"icon": "folder-opened",
									"type": "command",
									"command": "language-julia.cdHere"
								},
								{
									"key": "f",
									"name": "Execute file in REPL",
									"icon": "file",
									"type": "command",
									"command": "language-julia.executeFile"
								},
								{
									"key": "i",
									"name": "Start REPL",
									"icon": "repl",
									"type": "command",
									"command": "language-julia.startREPL"
								},
								{
									"key": "m",
									"name": "Execute code in REPL and move",
									"icon": "debug-continue",
									"type": "command",
									"command": "language-julia.executeCodeBlockOrSelectionAndMove"
								},
								{
									"key": "s",
									"name": "Execute code in REPL",
									"icon": "play",
									"type": "command",
									"command": "language-julia.executeJuliaCodeInREPL"
								},
								{
									"key": "C",
									"name": "Connect external REPL",
									"icon": "vm-connect",
									"type": "command",
									"command": "language-julia.connectREPL"
								},
								{
									"key": "D",
									"name": "Stop REPL",
									"icon": "stop",
									"type": "command",
									"command": "language-julia.stopREPL"
								},
								{
									"key": "F",
									"name": "Execute active file in REPL",
									"icon": "file",
									"type": "command",
									"command": "language-julia.executeActiveFile"
								}
							]
						}
					]
				},
				{
					"key": "languageId:latex",
					"name": "LaTeX",
					"type": "bindings",
					"bindings": [
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								}
							]
						},
						{
							"key": "b",
							"name": "+Backend",
							"icon": "circuit-board",
							"type": "bindings",
							"bindings": [
								{
									"key": "l",
									"name": "View Workshop Messages",
									"icon": "output",
									"type": "command",
									"command": "latex-workshop.log"
								},
								{
									"key": "m",
									"name": "Insert root magic comment",
									"icon": "comment",
									"type": "command",
									"command": "latex-workshop.addtexroot"
								},
								{
									"key": "s",
									"name": "Select the current environment name",
									"icon": "package",
									"type": "command",
									"command": "latex-workshop.select-envname"
								},
								{
									"key": "S",
									"name": "Select the current environment content",
									"icon": "package",
									"type": "command",
									"command": "latex-workshop.select-envcontent"
								}
							]
						},
						{
							"key": "c",
							"name": "+Build",
							"icon": "gear",
							"type": "bindings",
							"bindings": [
								{
									"key": "c",
									"name": "Build Project",
									"icon": "project",
									"type": "command",
									"command": "latex-workshop.build"
								},
								{
									"key": "i",
									"name": "Show compilation info",
									"icon": "info",
									"type": "command",
									"command": "latex-workshop.showCompilationPanel"
								},
								{
									"key": "k",
									"name": "Kill compiler process",
									"icon": "stop",
									"type": "command",
									"command": "latex-workshop.kill"
								},
								{
									"key": "l",
									"name": "Clean up auxiliary files",
									"icon": "trash",
									"type": "command",
									"command": "latex-workshop.clean"
								},
								{
									"key": "l",
									"name": "View compiler logs",
									"icon": "output",
									"type": "command",
									"command": "latex-workshop.compilerlog"
								},
								{
									"key": "r",
									"name": "Build with recipe",
									"icon": "heart",
									"type": "command",
									"command": "latex-workshop.recipes"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "e",
									"name": "Navigate to matching begin/end pair",
									"icon": "arrow-both",
									"type": "command",
									"command": "latex-workshop.navigate-envpair"
								}
							]
						},
						{
							"key": "i",
							"name": "+Insert",
							"icon": "add",
							"type": "bindings",
							"bindings": [
								{
									"key": "e",
									"name": "Close current environment",
									"icon": "close",
									"type": "command",
									"command": "latex-workshop.close-env"
								},
								{
									"key": "i",
									"name": "item",
									"icon": "list-unordered",
									"type": "command",
									"command": "latex-workshop.shortcut.item"
								},
								{
									"key": "w",
									"name": "Surround/wrap selection with begin/end",
									"icon": "selection",
									"type": "command",
									"command": "latex-workshop.wrap-env"
								}
							]
						},
						{
							"key": "l",
							"name": "+Bibtex",
							"icon": "book",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Align",
									"icon": "list-flat",
									"type": "command",
									"command": "latex-workshop.bibalign"
								},
								{
									"key": "s",
									"name": "Sort",
									"icon": "selection",
									"type": "command",
									"command": "latex-workshop.bibsort"
								},
								{
									"key": "S",
									"name": "Sort & Align",
									"icon": "list-tree",
									"type": "command",
									"command": "latex-workshop.bibalignsort"
								}
							]
						},
						{
							"key": "p",
							"name": "+Preview",
							"icon": "open-preview",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "View Document",
									"icon": "preview",
									"type": "command",
									"command": "latex-workshop.view"
								},
								{
									"key": "m",
									"name": "Toggle Math Preview Panel",
									"icon": "symbol-operator",
									"type": "command",
									"command": "latex-workshop.toggleMathPreviewPanel"
								},
								{
									"key": "p",
									"name": "SyncTeX from cursor",
									"icon": "open-preview",
									"type": "command",
									"command": "latex-workshop.synctex"
								},
								{
									"key": "r",
									"name": "Refresh all viewers",
									"icon": "refresh",
									"type": "command",
									"command": "latex-workshop.refresh-viewer"
								}
							]
						},
						{
							"key": "x",
							"name": "+Text",
							"icon": "symbol-text",
							"type": "bindings",
							"bindings": [
								{
									"key": "b",
									"name": "Bold",
									"icon": "bold",
									"type": "command",
									"command": "latex-workshop.shortcut.textbf"
								},
								{
									"key": "c",
									"name": "Small Caps",
									"icon": "preserve-case",
									"type": "command",
									"command": "latex-workshop.shortcut.textsc"
								},
								{
									"key": "e",
									"name": "Emphasis",
									"icon": "eye",
									"type": "command",
									"command": "latex-workshop.shortcut.emph"
								},
								{
									"key": "f",
									"name": "Sans Serif",
									"icon": "text-size",
									"type": "command",
									"command": "latex-workshop.shortcut.textsf"
								},
								{
									"key": "i",
									"name": "Italic",
									"icon": "italic",
									"type": "command",
									"command": "latex-workshop.shortcut.textit"
								},
								{
									"key": "n",
									"name": "Normal",
									"icon": "symbol-text",
									"type": "command",
									"command": "latex-workshop.shortcut.textnormal"
								},
								{
									"key": "r",
									"name": "Roman",
									"icon": "symbol-text",
									"type": "command",
									"command": "latex-workshop.shortcut.textrm"
								},
								{
									"key": "t",
									"name": "Terminal",
									"icon": "chevron-right",
									"type": "command",
									"command": "latex-workshop.shortcut.texttt"
								},
								{
									"key": "u",
									"name": "Underline",
									"icon": "remove",
									"type": "command",
									"command": "latex-workshop.shortcut.underline"
								},
								{
									"key": "m",
									"name": "+Math Fonts",
									"icon": "symbol-operator",
									"type": "bindings",
									"bindings": [
										{
											"key": "a",
											"name": "Calligraphic",
											"icon": "edit",
											"type": "command",
											"command": "latex-workshop.shortcut.mathcal"
										},
										{
											"key": "b",
											"name": "Bold",
											"icon": "bold",
											"type": "command",
											"command": "latex-workshop.shortcut.mathbf"
										},
										{
											"key": "f",
											"name": "Sans Serif",
											"icon": "text-size",
											"type": "command",
											"command": "latex-workshop.shortcut.mathsf"
										},
										{
											"key": "i",
											"name": "Italic",
											"icon": "italic",
											"type": "command",
											"command": "latex-workshop.shortcut.mathit"
										},
										{
											"key": "r",
											"name": "Roman",
											"icon": "symbol-text",
											"type": "command",
											"command": "latex-workshop.shortcut.mathrm"
										},
										{
											"key": "t",
											"name": "Terminal",
											"icon": "chevron-right",
											"type": "command",
											"command": "latex-workshop.shortcut.mathtt"
										}
									]
								}
							]
						}
					]
				},
				{
					"key": "languageId:markdown",
					"name": "Markdown",
					"type": "bindings",
					"bindings": [
						{
							"key": "c",
							"name": "+Buffer commands",
							"icon": "file",
							"type": "bindings",
							"bindings": [
								{
									"key": "e",
									"name": "Export to HTML",
									"icon": "file-code",
									"type": "command",
									"command": "markdown.extension.printToHtml"
								},
								{
									"key": "p",
									"name": "Open preview to the side",
									"icon": "open-preview",
									"type": "command",
									"command": "markdown.showPreviewToSide"
								},
								{
									"key": "P",
									"name": "Open preview in current group",
									"icon": "preview",
									"type": "command",
									"command": "markdown.showPreview"
								}
							]
						},
						{
							"key": "t",
							"name": "+Table of Contents",
							"icon": "list-tree",
							"type": "bindings",
							"bindings": [
								{
									"key": "c",
									"name": "Create Table of Contents",
									"icon": "list-tree",
									"type": "command",
									"command": "markdown.extension.toc.create"
								},
								{
									"key": "n",
									"name": "Add section numbers",
									"icon": "list-ordered",
									"type": "command",
									"command": "markdown.extension.toc.addSecNumbers"
								},
								{
									"key": "u",
									"name": "Update Table of Contents",
									"icon": "refresh",
									"type": "command",
									"command": "markdown.extension.toc.update"
								},
								{
									"key": "N",
									"name": "Remove section numbers",
									"icon": "list-unordered",
									"type": "command",
									"command": "markdown.extension.toc.removeSecNumbers"
								}
							]
						},
						{
							"key": "x",
							"name": "+Text",
							"icon": "symbol-text",
							"type": "bindings",
							"bindings": [
								{
									"key": "[",
									"name": "Decrease Heading level",
									"icon": "chevron-left",
									"type": "transient",
									"command": "markdown.extension.editing.toggleHeadingDown",
									"bindings": [
										{
											"key": "[",
											"name": "Decrease Heading level",
											"icon": "chevron-left",
											"type": "command",
											"command": "markdown.extension.editing.toggleHeadingDown"
										},
										{
											"key": "]",
											"name": "Increase Heading level",
											"icon": "chevron-right",
											"type": "command",
											"command": "markdown.extension.editing.toggleHeadingUp"
										}
									]
								},
								{
									"key": "]",
									"name": "Increase Heading level",
									"icon": "chevron-right",
									"type": "transient",
									"command": "markdown.extension.editing.toggleHeadingUp",
									"bindings": [
										{
											"key": "[",
											"name": "Decrease Heading level",
											"icon": "chevron-left",
											"type": "command",
											"command": "markdown.extension.editing.toggleHeadingDown"
										},
										{
											"key": "]",
											"name": "Increase Heading level",
											"icon": "chevron-right",
											"type": "command",
											"command": "markdown.extension.editing.toggleHeadingUp"
										}
									]
								},
								{
									"key": "`",
									"name": "Toggle inline code",
									"icon": "code",
									"type": "command",
									"command": "markdown.extension.editing.toggleCodeSpan"
								},
								{
									"key": "b",
									"name": "Toggle bold",
									"icon": "bold",
									"type": "command",
									"command": "markdown.extension.editing.toggleBold"
								},
								{
									"key": "i",
									"name": "Toggle italic",
									"icon": "italic",
									"type": "command",
									"command": "markdown.extension.editing.toggleItalic"
								},
								{
									"key": "l",
									"name": "Toggle list",
									"icon": "list-unordered",
									"type": "command",
									"command": "markdown.extension.editing.toggleList"
								},
								{
									"key": "m",
									"name": "Toggle math",
									"icon": "symbol-operator",
									"type": "command",
									"command": "markdown.extension.editing.toggleMath"
								},
								{
									"key": "s",
									"name": "Toggle strikethrough",
									"icon": "remove",
									"type": "command",
									"command": "markdown.extension.editing.toggleStrikethrough"
								},
								{
									"key": "~",
									"name": "Toggle code block",
									"icon": "file-code",
									"type": "command",
									"command": "markdown.extension.editing.toggleCodeBlock"
								}
							]
						}
					]
				},
				{
					"key": "languageId:objectpascal",
					"name": "ObjectPascal",
					"type": "bindings",
					"bindings": [
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "+Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "+Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.action.problems.focus"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "r",
									"name": "Go to references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in buffer",
									"icon": "file",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "S",
									"name": "Go to symbol in project",
									"icon": "project",
									"type": "command",
									"command": "workbench.action.showAllSymbols"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": ".",
									"name": "Quick fix",
									"icon": "lightbulb-autofix",
									"type": "command",
									"command": "editor.action.quickFix"
								},
								{
									"key": "r",
									"name": "Rename symbol",
									"icon": "symbol-keyword",
									"type": "command",
									"command": "editor.action.rename"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								}
							]
						}
					]
				},
				{
					"key": "languageId:php",
					"name": "PHP",
					"type": "bindings",
					"bindings": [
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "+Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "+Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.action.problems.focus"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "r",
									"name": "Go to references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in buffer",
									"icon": "file",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "S",
									"name": "Go to symbol in project",
									"icon": "project",
									"type": "command",
									"command": "workbench.action.showAllSymbols"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": ".",
									"name": "Quick fix",
									"icon": "lightbulb-autofix",
									"type": "command",
									"command": "editor.action.quickFix"
								},
								{
									"key": "r",
									"name": "Rename symbol",
									"icon": "symbol-keyword",
									"type": "command",
									"command": "editor.action.rename"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								}
							]
						}
					]
				},
				{
					"key": "languageId:python",
					"name": "Python",
					"type": "bindings",
					"bindings": [
						{
							"key": "v",
							"name": "+Virtualenv",
							"icon": "package",
							"type": "command",
							"command": "python.setInterpreter"
						},
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "+Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "+Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "b",
							"name": "+Backend",
							"icon": "circuit-board",
							"type": "bindings",
							"bindings": [
								{
									"key": "o",
									"name": "Show LSP output",
									"icon": "output",
									"type": "command",
									"command": "python.viewLanguageServerOutput"
								},
								{
									"key": "r",
									"name": "Restart LSP",
									"icon": "server-process",
									"type": "command",
									"command": "python.analysis.restartLanguageServer"
								}
							]
						},
						{
							"key": "c",
							"name": "+Execute",
							"icon": "play",
							"type": "bindings",
							"bindings": [
								{
									"key": "c",
									"name": "Execute file in terminal",
									"icon": "terminal",
									"type": "command",
									"command": "python.execInTerminal"
								},
								{
									"key": "C",
									"name": "Execute file in terminal",
									"icon": "terminal",
									"type": "command",
									"command": "python.execInTerminal"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.action.problems.focus"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "r",
									"name": "Go to references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in file",
									"icon": "file",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "S",
									"name": "Go to symbol in project",
									"icon": "project",
									"type": "command",
									"command": "workbench.action.showAllSymbols"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": ".",
									"name": "Refactor menu",
									"icon": "lightbulb",
									"type": "command",
									"command": "editor.action.refactor"
								},
								{
									"key": "I",
									"name": "Sort imports",
									"icon": "selection",
									"type": "command",
									"command": "python.sortImports"
								}
							]
						},
						{
							"key": "s",
							"name": "+REPL",
							"icon": "repl",
							"type": "bindings",
							"bindings": [
								{
									"key": "i",
									"name": "Start REPL",
									"icon": "repl",
									"type": "command",
									"command": "python.startREPL"
								},
								{
									"key": "l",
									"name": "Send line/selection to REPL",
									"icon": "selection",
									"type": "command",
									"command": "python.execSelectionInTerminal"
								},
								{
									"key": "r",
									"name": "Send line/selection to REPL",
									"icon": "selection",
									"type": "command",
									"command": "python.execSelectionInTerminal"
								}
							]
						},
						{
							"key": "t",
							"name": "+Test",
							"icon": "beaker",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Run all tests",
									"icon": "beaker",
									"type": "command",
									"command": "testing.runAll"
								},
								{
									"key": "b",
									"name": "Run current test file",
									"icon": "file",
									"type": "command",
									"command": "testing.runCurrentFile"
								},
								{
									"key": "r",
									"name": "Re-run failed tests",
									"icon": "close",
									"type": "command",
									"command": "testing.reRunFailTests"
								},
								{
									"key": "t",
									"name": "Select and run test",
									"icon": "list-unordered",
									"type": "command",
									"command": "testing.runSelected"
								},
								{
									"key": "A",
									"name": "Debug all tests",
									"icon": "bug",
									"type": "command",
									"command": "testing.debugAll"
								},
								{
									"key": "T",
									"name": "Select and debug test",
									"icon": "debug-alt",
									"type": "command",
									"command": "testing.debugSelected"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								}
							]
						}
					]
				},
				{
					"key": "languageId:quarto",
					"name": "quarto",
					"type": "bindings",
					"bindings": [
						{
							"key": "d",
							"name": "Debugonce R",
							"type": "command",
							"icon": "debug",
							"command": "r.runCommandWithSelectionOrWord",
							"args": "debugonce($$)"
						},
						{
							"key": "h",
							"name": "Help R",
							"icon": "question",
							"type": "command",
							"command": "r.helpPanel.openForSelection"
						},
						{
							"key": "i",
							"name": "Insert cell",
							"type": "command",
							"icon": "list-flat",
							"command": "quarto.insertCodeCell"
						},
						{
							"key": "m",
							"name": "Run current cell",
							"icon": "play",
							"type": "command",
							"command": "quarto.runCurrentCell"
						},
						{
							"key": "o",
							"name": "Objects in workspace R",
							"type": "command",
							"icon": "symbol-field",
							"command": "r.runCommand",
							"args": "sort(sapply(ls(), function(x){object.size(get(x))})) "
						},
						{
							"key": "p",
							"name": "Render",
							"type": "command",
							"icon": "check",
							"command": "quarto.render"
						},
						{
							"key": "s",
							"name": "Run selection",
							"icon": "selection",
							"type": "command",
							"command": "quarto.runSelection"
						},
						{
							"key": "R",
							"name": "Restart R",
							"type": "command",
							"icon": "debug-restart",
							"command": "r.runCommand",
							"args": "rstudioapi::restartSession()"
						},
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "a",
							"name": "+Code actions",
							"icon": "zap",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Execute code action",
									"icon": "lightbulb",
									"type": "command",
									"command": "editor.action.codeAction"
								},
								{
									"key": "f",
									"name": "Execute fix action",
									"icon": "lightbulb-autofix",
									"type": "command",
									"command": "editor.action.quickFix"
								},
								{
									"key": "r",
									"name": "Refactor action",
									"icon": "edit",
									"type": "command",
									"command": "editor.action.refactor"
								},
								{
									"key": "s",
									"name": "Source action",
									"icon": "lightbulb",
									"type": "command",
									"command": "editor.action.sourceAction"
								}
							]
						},
						{
							"key": "f",
							"name": "+Fold",
							"icon": "fold",
							"type": "bindings",
							"bindings": [
								{
									"key": "f",
									"name": "Fold cell",
									"icon": "fold",
									"type": "command",
									"command": "editor.fold"
								},
								{
									"key": "u",
									"name": "Unfold cell",
									"icon": "unfold",
									"type": "command",
									"command": "editor.unfold"
								},
								{
									"key": "F",
									"name": "Fold all cells",
									"icon": "fold",
									"type": "command",
									"command": "editor.foldAll"
								},
								{
									"key": "U",
									"name": "Unfold all cells",
									"icon": "unfold",
									"type": "command",
									"command": "editor.unfoldAll"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to declaration",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.revealDeclaration"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.actions.view.problems"
								},
								{
									"key": "f",
									"name": "Go to file in explorer",
									"icon": "file",
									"type": "command",
									"command": "workbench.files.action.showActiveFileInExplorer"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "r",
									"name": "Go to reference",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in buffer",
									"icon": "symbol-class",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "S",
									"name": "Go to symbol in project",
									"icon": "symbol-class",
									"type": "command",
									"command": "workbench.action.showAllSymbols"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": "r",
									"name": "Rename Symbol",
									"icon": "symbol-keyword",
									"type": "command",
									"command": "editor.action.rename"
								}
							]
						},
						{
							"key": "v",
							"name": "+View R",
							"icon": "preview",
							"type": "bindings",
							"bindings": [
								{
									"key": "c",
									"name": "Column numbers",
									"type": "command",
									"icon": "list-ordered",
									"command": "r.runCommandWithSelectionOrWord",
									"args": "ncol($$)"
								},
								{
									"key": "h",
									"name": "head",
									"type": "command",
									"icon": "list-filter",
									"command": "r.head"
								},
								{
									"key": "l",
									"name": "length",
									"type": "command",
									"icon": "list-ordered",
									"command": "r.length"
								},
								{
									"key": "n",
									"name": "Names",
									"type": "command",
									"icon": "symbol-parameter",
									"command": "r.names"
								},
								{
									"key": "p",
									"name": "print",
									"icon": "symbol-field",
									"type": "command",
									"command": "r.runCommandWithSelectionOrWord",
									"args": "$$"
								},
								{
									"key": "r",
									"name": "Row numbers",
									"type": "command",
									"icon": "list-ordered",
									"command": "r.nrow"
								},
								{
									"key": "s",
									"name": "str",
									"type": "command",
									"icon": "list-flat",
									"command": "r.runCommandWithSelectionOrWord",
									"args": "str($$)"
								},
								{
									"key": "v",
									"name": "View",
									"type": "command",
									"icon": "preview",
									"command": "r.view"
								},
								{
									"key": "C",
									"name": "Column names",
									"type": "command",
									"icon": "symbol-key",
									"command": "r.runCommandWithSelectionOrWord",
									"args": "colnames($$)"
								},
								{
									"key": "R",
									"name": "Row names",
									"type": "command",
									"icon": "preserve-case",
									"command": "r.runCommandWithSelectionOrWord",
									"args": "rownames($$)"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek declaration",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.peekDeclaration"
								},
								{
									"key": "g",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								}
							]
						}
					]
				},
				{
					"key": "languageId:r",
					"name": "R",
					"type": "bindings",
					"bindings": [
						{
							"key": "d",
							"name": "Debugonce",
							"type": "command",
							"icon": "debug",
							"command": "r.runCommandWithSelectionOrWord",
							"args": "debugonce($$)"
						},
						{
							"key": "h",
							"name": "Help",
							"icon": "question",
							"type": "command",
							"command": "r.helpPanel.openForSelection"
						},
						{
							"key": "o",
							"name": "Objects in workspace R",
							"type": "command",
							"icon": "symbol-field",
							"command": "r.runCommand",
							"args": "sort(sapply(ls(), function(x){object.size(get(x))})) "
						},
						{
							"key": "s",
							"name": "Run selection",
							"icon": "play",
							"type": "command",
							"command": "r.runSelection"
						},
						{
							"key": "R",
							"name": "Restart R",
							"type": "command",
							"icon": "debug-restart",
							"command": "r.runCommand",
							"args": "rstudioapi::restartSession()"
						},
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "a",
							"name": "+Code actions",
							"icon": "zap",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Execute code action",
									"icon": "lightbulb",
									"type": "command",
									"command": "editor.action.codeAction"
								},
								{
									"key": "f",
									"name": "Execute fix action",
									"icon": "lightbulb-autofix",
									"type": "command",
									"command": "editor.action.quickFix"
								},
								{
									"key": "r",
									"name": "Refactor action",
									"icon": "edit",
									"type": "command",
									"command": "editor.action.refactor"
								},
								{
									"key": "s",
									"name": "Source action",
									"icon": "lightbulb",
									"type": "command",
									"command": "editor.action.sourceAction"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to declaration",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.revealDeclaration"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.actions.view.problems"
								},
								{
									"key": "f",
									"name": "Go to file in explorer",
									"icon": "file",
									"type": "command",
									"command": "workbench.files.action.showActiveFileInExplorer"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "r",
									"name": "Go to reference",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in buffer",
									"icon": "symbol-class",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "S",
									"name": "Go to symbol in project",
									"icon": "symbol-class",
									"type": "command",
									"command": "workbench.action.showAllSymbols"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": "r",
									"name": "Rename Symbol",
									"icon": "symbol-keyword",
									"type": "command",
									"command": "editor.action.rename"
								}
							]
						},
						{
							"key": "v",
							"name": "+View",
							"icon": "preview",
							"type": "bindings",
							"bindings": [
								{
									"key": "c",
									"name": "Column numbers",
									"type": "command",
									"icon": "list-ordered",
									"command": "r.runCommandWithSelectionOrWord",
									"args": "ncol($$)"
								},
								{
									"key": "h",
									"name": "head",
									"type": "command",
									"icon": "list-filter",
									"command": "r.head"
								},
								{
									"key": "l",
									"name": "length",
									"type": "command",
									"icon": "list-ordered",
									"command": "r.length"
								},
								{
									"key": "n",
									"name": "Names",
									"type": "command",
									"icon": "symbol-parameter",
									"command": "r.names"
								},
								{
									"key": "p",
									"name": "print",
									"icon": "symbol-field",
									"type": "command",
									"command": "r.runCommandWithSelectionOrWord",
									"args": "$$"
								},
								{
									"key": "r",
									"name": "Row numbers",
									"type": "command",
									"icon": "list-ordered",
									"command": "r.nrow"
								},
								{
									"key": "s",
									"name": "str",
									"type": "command",
									"icon": "list-flat",
									"command": "r.runCommandWithSelectionOrWord",
									"args": "str($$)"
								},
								{
									"key": "v",
									"name": "View",
									"type": "command",
									"icon": "preview",
									"command": "r.view"
								},
								{
									"key": "C",
									"name": "Column names",
									"type": "command",
									"icon": "symbol-key",
									"command": "r.runCommandWithSelectionOrWord",
									"args": "colnames($$)"
								},
								{
									"key": "R",
									"name": "Row names",
									"type": "command",
									"icon": "preserve-case",
									"command": "r.runCommandWithSelectionOrWord",
									"args": "rownames($$)"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek declaration",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.peekDeclaration"
								},
								{
									"key": "g",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								}
							]
						}
					]
				},
				{
					"key": "languageId:ruby",
					"name": "Ruby",
					"type": "bindings",
					"bindings": [
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "+Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "+Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.action.problems.focus"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "r",
									"name": "Go to references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in buffer",
									"icon": "file",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "S",
									"name": "Go to symbol in project",
									"icon": "project",
									"type": "command",
									"command": "workbench.action.showAllSymbols"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": "r",
									"name": "Rename symbol",
									"icon": "symbol-keyword",
									"type": "command",
									"command": "editor.action.rename"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								}
							]
						}
					]
				},
				{
					"key": "languageId:rust",
					"name": "Rust",
					"type": "bindings",
					"bindings": [
						{
							"key": "T",
							"name": "Toggle inlay hints",
							"icon": "book",
							"type": "command",
							"command": "rust-analyzer.toggleInlayHints"
						},
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.format"
								}
							]
						},
						{
							"key": "a",
							"name": "+Actions",
							"icon": "zap",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Execute code action",
									"icon": "lightbulb",
									"type": "command",
									"command": "editor.action.codeAction"
								},
								{
									"key": "f",
									"name": "Execute fix action",
									"icon": "lightbulb-autofix",
									"type": "command",
									"command": "editor.action.quickFix"
								},
								{
									"key": "s",
									"name": "Execute source action",
									"icon": "lightbulb",
									"type": "command",
									"command": "editor.action.sourceAction"
								},
								{
									"key": "r",
									"name": "+Refactor",
									"icon": "edit",
									"type": "bindings",
									"bindings": [
										{
											"key": ".",
											"name": "Execute refactor action",
											"icon": "lightbulb-autofix",
											"type": "command",
											"command": "editor.action.refactor"
										},
										{
											"key": "r",
											"name": "Rename symbol",
											"icon": "symbol-keyword",
											"type": "command",
											"command": "editor.action.rename"
										}
									]
								}
							]
						},
						{
							"key": "b",
							"name": "+Backend",
							"icon": "circuit-board",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Rust analyzer: describe status",
									"icon": "dashboard",
									"type": "command",
									"command": "rust-analyzer.analyzerStatus"
								},
								{
									"key": "r",
									"name": "Rust analyzer: restart server",
									"icon": "server-process",
									"type": "command",
									"command": "rust-analyzer.reload"
								},
								{
									"key": "v",
									"name": "Rust analyzer: Show version",
									"icon": "info",
									"type": "command",
									"command": "rust-analyzer.serverVersion"
								},
								{
									"key": "R",
									"name": "Rust analyzer: reload workspace",
									"icon": "refresh",
									"type": "command",
									"command": "rust-analyzer.reloadWorkspace"
								}
							]
						},
						{
							"key": "g",
							"name": "+Goto",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "h",
									"name": "Show call hierarchy",
									"icon": "type-hierarchy",
									"type": "command",
									"command": "references-view.showCallHierarchy"
								},
								{
									"key": "i",
									"name": "Go to implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.goToImplementation"
								},
								{
									"key": "r",
									"name": "Go to references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in buffer",
									"icon": "file",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "t",
									"name": "Go to type definition",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.goToTypeDefinition"
								},
								{
									"key": "I",
									"name": "Find implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "references-view.findImplementations"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "S",
									"name": "Go to symbol in project",
									"icon": "project",
									"type": "command",
									"command": "workbench.action.showAllSymbols"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "h",
									"name": "Peek call hierarchy",
									"icon": "type-hierarchy",
									"type": "command",
									"command": "editor.showCallHierarchy"
								},
								{
									"key": "i",
									"name": "Peek implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.peekImplementation"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								}
							]
						}
					]
				},
				{
					"key": "languageId:typescript",
					"name": "TypeScript",
					"type": "bindings",
					"bindings": [
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "+Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "+Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "h",
									"name": "Show call hierarchy",
									"icon": "type-hierarchy",
									"type": "command",
									"command": "references-view.showCallHierarchy"
								},
								{
									"key": "r",
									"name": "Go to reference",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in buffer",
									"icon": "file",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "t",
									"name": "Go to type definition",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.goToTypeDefinition"
								},
								{
									"key": "I",
									"name": "Find implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "references-view.findImplementations"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "S",
									"name": "Go to symbol in project",
									"icon": "project",
									"type": "command",
									"command": "workbench.action.showAllSymbols"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "h",
									"name": "Peek call hierarchy",
									"icon": "type-hierarchy",
									"type": "command",
									"command": "editor.showCallHierarchy"
								},
								{
									"key": "i",
									"name": "Peek implementations",
									"icon": "symbol-module",
									"type": "command",
									"command": "editor.action.peekImplementation"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								},
								{
									"key": "t",
									"name": "Peek type definition",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.peekTypeDefinition"
								}
							]
						}
					]
				},
				{
					"key": "languageId:cuda-cpp",
					"name": "CUDA-C++",
					"type": "bindings",
					"bindings": [
						{
							"key": "=",
							"name": "+Format",
							"icon": "list-flat",
							"type": "bindings",
							"bindings": [
								{
									"key": "=",
									"name": "Format region or buffer",
									"icon": "list-flat",
									"type": "command",
									"command": "editor.action.format"
								},
								{
									"key": "b",
									"name": "Format buffer",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument"
								},
								{
									"key": "c",
									"name": "Format changes",
									"icon": "diff",
									"type": "command",
									"command": "editor.action.formatChanges"
								},
								{
									"key": "s",
									"name": "Format selection",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection"
								},
								{
									"key": "B",
									"name": "Format buffer with formatter",
									"icon": "file",
									"type": "command",
									"command": "editor.action.formatDocument.multiple"
								},
								{
									"key": "S",
									"name": "Format selection with formatter",
									"icon": "selection",
									"type": "command",
									"command": "editor.action.formatSelection.multiple"
								}
							]
						},
						{
							"key": "b",
							"name": "+Backend",
							"icon": "circuit-board",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Reset Database",
									"icon": "database",
									"type": "command",
									"command": "C_Cpp.ResetDatabase"
								},
								{
									"key": "w",
									"name": "Rescan Workspace",
									"icon": "project",
									"type": "command",
									"command": "C_Cpp.RescanWorkspace"
								}
							]
						},
						{
							"key": "d",
							"name": "+Debug",
							"icon": "bug",
							"type": "bindings",
							"bindings": [
								{
									"key": "f",
									"name": "Change debug focus",
									"icon": "eye-watch",
									"type": "command",
									"command": "cuda.changeDebugFocus"
								}
							]
						},
						{
							"key": "g",
							"name": "+Go to",
							"icon": "go-to-file",
							"type": "bindings",
							"bindings": [
								{
									"key": "a",
									"name": "Switch Header/Source",
									"icon": "files",
									"type": "command",
									"command": "C_Cpp.SwitchHeaderSource"
								},
								{
									"key": "d",
									"name": "Go to declaration",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.revealDeclaration"
								},
								{
									"key": "e",
									"name": "Go to errors/problems",
									"icon": "error",
									"type": "command",
									"command": "workbench.actions.view.problems"
								},
								{
									"key": "f",
									"name": "Go to file in explorer",
									"icon": "file",
									"type": "command",
									"command": "workbench.files.action.showActiveFileInExplorer"
								},
								{
									"key": "g",
									"name": "Go to definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.revealDefinition"
								},
								{
									"key": "r",
									"name": "Go to reference",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.goToReferences"
								},
								{
									"key": "s",
									"name": "Go to symbol in buffer",
									"icon": "symbol-class",
									"type": "command",
									"command": "workbench.action.gotoSymbol"
								},
								{
									"key": "R",
									"name": "Find references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "references-view.findReferences"
								},
								{
									"key": "S",
									"name": "Go to symbol in project",
									"icon": "symbol-class",
									"type": "command",
									"command": "workbench.action.showAllSymbols"
								}
							]
						},
						{
							"key": "r",
							"name": "+Refactor",
							"icon": "edit",
							"type": "bindings",
							"bindings": [
								{
									"key": "r",
									"name": "Rename Symbol",
									"icon": "symbol-keyword",
									"type": "command",
									"command": "editor.action.rename"
								}
							]
						},
						{
							"key": "G",
							"name": "+Peek",
							"icon": "eye",
							"type": "bindings",
							"bindings": [
								{
									"key": "d",
									"name": "Peek declaration",
									"icon": "symbol-struct",
									"type": "command",
									"command": "editor.action.peekDeclaration"
								},
								{
									"key": "g",
									"name": "Peek definition",
									"icon": "symbol-function",
									"type": "command",
									"command": "editor.action.peekDefinition"
								},
								{
									"key": "r",
									"name": "Peek references",
									"icon": "symbol-reference",
									"type": "command",
									"command": "editor.action.referenceSearch.trigger"
								}
							]
						}
					]
				}
			]
		},
		{
			"key": "p",
			"name": "+Project",
			"icon": "project",
			"type": "bindings",
			"bindings": [
				{
					"key": "c",
					"name": "Compile project",
					"icon": "gear",
					"type": "command",
					"command": "workbench.action.tasks.build"
				},
				{
					"key": "f",
					"name": "+Find file in project",
					"icon": "file",
					"type": "command",
					"command": "workbench.action.quickOpen"
				},
				{
					"key": "l",
					"name": "+Switch project",
					"icon": "project",
					"type": "command",
					"command": "workbench.action.openRecent"
				},
				{
					"key": "p",
					"name": "+Switch project",
					"icon": "project",
					"type": "command",
					"command": "workbench.action.openRecent"
				},
				{
					"key": "t",
					"name": "Show tree/explorer view",
					"icon": "list-tree",
					"type": "command",
					"command": "workbench.view.explorer"
				},
				{
					"key": "R",
					"name": "+Replace in files",
					"icon": "find-replace",
					"type": "command",
					"command": "workbench.action.replaceInFiles"
				},
				{
					"key": "T",
					"name": "Test project",
					"icon": "beaker",
					"type": "command",
					"command": "workbench.action.tasks.test"
				}
			]
		},
		{
			"key": "q",
			"name": "+Quit",
			"icon": "x",
			"type": "bindings",
			"bindings": [
				{
					"key": "f",
					"name": "Close frame",
					"icon": "close",
					"type": "command",
					"command": "workbench.action.closeWindow"
				},
				{
					"key": "q",
					"name": "Close frame",
					"icon": "close",
					"type": "command",
					"command": "workbench.action.closeWindow"
				},
				{
					"key": "r",
					"name": "Reload frame",
					"icon": "refresh",
					"type": "command",
					"command": "workbench.action.reloadWindow"
				},
				{
					"key": "s",
					"name": "Save all and close frame",
					"icon": "save-all",
					"type": "commands",
					"commands": [
						"workbench.action.files.saveAll",
						"workbench.action.closeWindow"
					]
				},
				{
					"key": "Q",
					"name": "Quit application",
					"icon": "log-out",
					"type": "command",
					"command": "workbench.action.quit"
				},
				{
					"key": "R",
					"name": "Reload frame with extensions disabled",
					"icon": "refresh",
					"type": "command",
					"command": "workbench.action.reloadWindowWithExtensionsDisabled"
				}
			]
		},
		{
			"key": "r",
			"name": "+Resume/Repeat",
			"icon": "clock",
			"type": "bindings",
			"bindings": [
				{
					"key": ".",
					"name": "Repeat recent actions",
					"icon": "redo",
					"type": "command",
					"command": "whichkey.repeatRecent",
					"args": "vspacecode.bindings"
				},
				{
					"key": "b",
					"name": "Recent buffers",
					"icon": "versions",
					"type": "command",
					"command": "workbench.action.showAllEditorsByMostRecentlyUsed"
				},
				{
					"key": "s",
					"name": "Search in project",
					"icon": "search",
					"type": "command",
					"command": "workbench.action.findInFiles"
				}
			]
		},
		{
			"key": "s",
			"name": "+Search/Symbol",
			"icon": "search",
			"type": "bindings",
			"bindings": [
				{
					"key": "c",
					"name": "Clear highlight",
					"icon": "clear-all",
					"type": "command",
					"command": "vim.remap",
					"args": {
						"commands": [
							{
								"command": ":noh"
							}
						]
					}
				},
				{
					"key": "e",
					"name": "Edit symbol",
					"icon": "edit",
					"type": "command",
					"command": "editor.action.rename"
				},
				{
					"key": "h",
					"name": "Highlight symbol",
					"icon": "symbol-color",
					"type": "transient",
					"command": "editor.action.wordHighlight.trigger",
					"bindings": [
						{
							"key": "/",
							"name": "Search in project with selection",
							"icon": "selection",
							"type": "commands",
							"commands": [
								"editor.action.addSelectionToNextFindMatch",
								"workbench.action.findInFiles"
							]
						},
						{
							"key": "n",
							"name": "Next occurrence",
							"icon": "arrow-down",
							"type": "command",
							"command": "editor.action.wordHighlight.next"
						},
						{
							"key": "p",
							"name": "Previous occurrence",
							"icon": "arrow-up",
							"type": "command",
							"command": "editor.action.wordHighlight.prev"
						},
						{
							"key": "N",
							"name": "Previous occurrence",
							"icon": "arrow-up",
							"type": "command",
							"command": "editor.action.wordHighlight.prev"
						}
					]
				},
				{
					"key": "j",
					"name": "Jump to symbol in buffer",
					"icon": "symbol-class",
					"type": "command",
					"command": "workbench.action.gotoSymbol"
				},
				{
					"key": "p",
					"name": "Search in project",
					"icon": "search",
					"type": "command",
					"command": "workbench.action.findInFiles"
				},
				{
					"key": "r",
					"name": "Search all references",
					"icon": "references",
					"type": "command",
					"command": "editor.action.referenceSearch.trigger"
				},
				{
					"key": "s",
					"name": "Fuzzy search in current buffer",
					"icon": "file",
					"type": "command",
					"command": "fuzzySearch.activeTextEditorWithCurrentSelection"
				},
				{
					"key": "J",
					"name": "Jump to symbol in project",
					"icon": "symbol-class",
					"type": "command",
					"command": "workbench.action.showAllSymbols"
				},
				{
					"key": "P",
					"name": "Search in project with selection",
					"icon": "selection",
					"type": "commands",
					"commands": [
						"editor.action.addSelectionToNextFindMatch",
						"workbench.action.findInFiles"
					]
				},
				{
					"key": "R",
					"name": "Search all references in side bar",
					"icon": "references",
					"type": "command",
					"command": "references-view.find"
				},
				{
					"key": "S",
					"name": "Fuzzy search with selection in current buffer",
					"icon": "selection",
					"type": "commands",
					"commands": [
						"editor.action.addSelectionToNextFindMatch",
						"fuzzySearch.activeTextEditorWithCurrentSelection"
					]
				}
			]
		},
		{
			"key": "t",
			"name": "+Toggles",
			"icon": "settings",
			"type": "bindings",
			"bindings": [
				{
					"key": "c",
					"name": "Toggle find case sensitive",
					"icon": "case-sensitive",
					"type": "command",
					"command": "toggleFindCaseSensitive"
				},
				{
					"key": "l",
					"name": "Toggle word wrap",
					"icon": "word-wrap",
					"type": "command",
					"command": "editor.action.toggleWordWrap"
				},
				{
					"key": "w",
					"name": "Toggle render whitespace",
					"icon": "whitespace",
					"type": "command",
					"command": "editor.action.toggleRenderWhitespace"
				}
			]
		},
		{
			"key": "w",
			"name": "+Window",
			"icon": "split-horizontal",
			"type": "bindings",
			"bindings": [
				{
					"key": "-",
					"name": "Split window below",
					"icon": "split-vertical",
					"type": "command",
					"command": "workbench.action.splitEditorDown"
				},
				{
					"key": "/",
					"name": "Split window right",
					"icon": "split-horizontal",
					"type": "command",
					"command": "workbench.action.splitEditor"
				},
				{
					"key": "=",
					"name": "Reset window sizes",
					"icon": "move",
					"type": "command",
					"command": "workbench.action.evenEditorWidths"
				},
				{
					"key": "[",
					"name": "Shrink window",
					"icon": "remove",
					"type": "transient",
					"command": "workbench.action.decreaseViewSize",
					"bindings": [
						{
							"key": "[",
							"name": "Shrink window",
							"icon": "remove",
							"type": "command",
							"command": "workbench.action.decreaseViewSize"
						},
						{
							"key": "]",
							"name": "Enlarge window",
							"icon": "add",
							"type": "command",
							"command": "workbench.action.increaseViewSize"
						}
					]
				},
				{
					"key": "]",
					"name": "Enlarge window",
					"icon": "add",
					"type": "transient",
					"command": "workbench.action.increaseViewSize",
					"bindings": [
						{
							"key": "[",
							"name": "Shrink window",
							"icon": "remove",
							"type": "command",
							"command": "workbench.action.decreaseViewSize"
						},
						{
							"key": "]",
							"name": "Enlarge window",
							"icon": "add",
							"type": "command",
							"command": "workbench.action.increaseViewSize"
						}
					]
				},
				{
					"key": "d",
					"name": "Close window",
					"icon": "close",
					"type": "command",
					"command": "workbench.action.closeEditorsInGroup"
				},
				{
					"key": "h",
					"name": "Focus window left",
					"icon": "arrow-left",
					"type": "command",
					"command": "workbench.action.navigateLeft"
				},
				{
					"key": "j",
					"name": "Focus window down",
					"icon": "arrow-down",
					"type": "command",
					"command": "workbench.action.navigateDown"
				},
				{
					"key": "k",
					"name": "Focus window up",
					"icon": "arrow-up",
					"type": "command",
					"command": "workbench.action.navigateUp"
				},
				{
					"key": "l",
					"name": "Focus window right",
					"icon": "arrow-right",
					"type": "command",
					"command": "workbench.action.navigateRight"
				},
				{
					"key": "m",
					"name": "Maximize window",
					"icon": "screen-full",
					"type": "command",
					"command": "workbench.action.toggleMaximizeEditorGroup"
				},
				{
					"key": "o",
					"name": "Switch frame",
					"icon": "multiple-windows",
					"type": "command",
					"command": "workbench.action.quickSwitchWindow"
				},
				{
					"key": "s",
					"name": "Split window below",
					"icon": "split-vertical",
					"type": "command",
					"command": "workbench.action.splitEditorDown"
				},
				{
					"key": "v",
					"name": "Split window right",
					"icon": "split-horizontal",
					"type": "command",
					"command": "workbench.action.splitEditor"
				},
				{
					"key": "w",
					"name": "Focus next window",
					"icon": "arrow-small-down",
					"type": "command",
					"command": "workbench.action.focusNextGroup"
				},
				{
					"key": "x",
					"name": "Close all windows",
					"icon": "close-all",
					"type": "command",
					"command": "workbench.action.closeAllGroups"
				},
				{
					"key": "z",
					"name": "Combine all buffers",
					"icon": "combine",
					"type": "command",
					"command": "workbench.action.joinAllGroups"
				},
				{
					"key": "D",
					"name": "Close all other windows",
					"icon": "close-all",
					"type": "command",
					"command": "workbench.action.closeEditorsInOtherGroups"
				},
				{
					"key": "F",
					"name": "Open new empty frame",
					"icon": "empty-window",
					"type": "command",
					"command": "workbench.action.newWindow"
				},
				{
					"key": "H",
					"name": "Move window left",
					"icon": "triangle-left",
					"type": "command",
					"command": "workbench.action.moveActiveEditorGroupLeft"
				},
				{
					"key": "J",
					"name": "Move window down",
					"icon": "triangle-down",
					"type": "command",
					"command": "workbench.action.moveActiveEditorGroupDown"
				},
				{
					"key": "K",
					"name": "Move window up",
					"icon": "triangle-up",
					"type": "command",
					"command": "workbench.action.moveActiveEditorGroupUp"
				},
				{
					"key": "L",
					"name": "Move window right",
					"icon": "triangle-right",
					"type": "command",
					"command": "workbench.action.moveActiveEditorGroupRight"
				},
				{
					"key": "M",
					"name": "Maximize window without hiding others",
					"icon": "chrome-maximize",
					"type": "command",
					"command": "workbench.action.toggleEditorWidths"
				},
				{
					"key": "W",
					"name": "Focus previous window",
					"icon": "arrow-small-up",
					"type": "command",
					"command": "workbench.action.focusPreviousGroup"
				}
			]
		},
		{
			"key": "x",
			"name": "+Text",
			"icon": "symbol-text",
			"type": "bindings",
			"bindings": [
				{
					"key": ".",
					"name": "Quick fix",
					"icon": "lightbulb-autofix",
					"type": "command",
					"command": "editor.action.quickFix"
				},
				{
					"key": "a",
					"name": "Find all references",
					"icon": "references",
					"type": "command",
					"command": "editor.action.referenceSearch.trigger"
				},
				{
					"key": "i",
					"name": "Organize Imports",
					"icon": "selection",
					"type": "command",
					"command": "editor.action.organizeImports"
				},
				{
					"key": "o",
					"name": "Open link",
					"icon": "link-external",
					"type": "command",
					"command": "editor.action.openLink"
				},
				{
					"key": "r",
					"name": "Rename symbol",
					"icon": "symbol-keyword",
					"type": "command",
					"command": "editor.action.rename"
				},
				{
					"key": "u",
					"name": "To lower case",
					"icon": "case-sensitive",
					"type": "command",
					"command": "editor.action.transformToLowercase"
				},
				{
					"key": "J",
					"name": "Move lines down",
					"icon": "triangle-down",
					"type": "transient",
					"command": "editor.action.moveLinesDownAction",
					"bindings": [
						{
							"key": "J",
							"name": "Move lines down",
							"icon": "triangle-down",
							"type": "command",
							"command": "editor.action.moveLinesDownAction"
						},
						{
							"key": "K",
							"name": "Move lines up",
							"icon": "triangle-up",
							"type": "command",
							"command": "editor.action.moveLinesUpAction"
						}
					]
				},
				{
					"key": "K",
					"name": "Move lines up",
					"icon": "triangle-up",
					"type": "transient",
					"command": "editor.action.moveLinesUpAction",
					"bindings": [
						{
							"key": "J",
							"name": "Move lines down",
							"icon": "triangle-down",
							"type": "command",
							"command": "editor.action.moveLinesDownAction"
						},
						{
							"key": "K",
							"name": "Move lines up",
							"icon": "triangle-up",
							"type": "command",
							"command": "editor.action.moveLinesUpAction"
						}
					]
				},
				{
					"key": "R",
					"name": "Refactor",
					"icon": "edit",
					"type": "command",
					"command": "editor.action.refactor"
				},
				{
					"key": "U",
					"name": "To upper case",
					"icon": "preserve-case",
					"type": "command",
					"command": "editor.action.transformToUppercase"
				},
				{
					"key": "d",
					"name": "+Delete",
					"icon": "trash",
					"type": "bindings",
					"bindings": [
						{
							"key": "w",
							"name": "Delete trailing whitespace",
							"icon": "whitespace",
							"type": "command",
							"command": "editor.action.trimTrailingWhitespace"
						}
					]
				},
				{
					"key": "l",
					"name": "+Lines",
					"icon": "list-flat",
					"type": "bindings",
					"bindings": [
						{
							"key": "d",
							"name": "Duplicate lines down",
							"icon": "fold-down",
							"type": "command",
							"command": "editor.action.copyLinesDownAction"
						},
						{
							"key": "s",
							"name": "Sort lines in ascending order",
							"icon": "chevron-left",
							"type": "command",
							"command": "editor.action.sortLinesAscending"
						},
						{
							"key": "D",
							"name": "Duplicate lines up",
							"icon": "fold-up",
							"type": "command",
							"command": "editor.action.copyLinesUpAction"
						},
						{
							"key": "S",
							"name": "Sort lines in descending order",
							"icon": "chevron-right",
							"type": "command",
							"command": "editor.action.sortLinesDescending"
						}
					]
				},
				{
					"key": "m",
					"name": "+Merge conflict",
					"icon": "git-merge",
					"type": "bindings",
					"bindings": [
						{
							"key": "b",
							"name": "Accept both",
							"icon": "arrow-both",
							"type": "command",
							"command": "merge-conflict.accept.both"
						},
						{
							"key": "c",
							"name": "Accept current",
							"icon": "arrow-small-right",
							"type": "command",
							"command": "merge-conflict.accept.current"
						},
						{
							"key": "i",
							"name": "Accept incoming",
							"icon": "arrow-small-left",
							"type": "command",
							"command": "merge-conflict.accept.incoming"
						},
						{
							"key": "k",
							"name": "Compare current conflict",
							"icon": "diff",
							"type": "command",
							"command": "merge-conflict.compare"
						},
						{
							"key": "n",
							"name": "Next Conflict",
							"icon": "arrow-down",
							"type": "command",
							"command": "merge-conflict.next"
						},
						{
							"key": "s",
							"name": "Accept selection",
							"icon": "selection",
							"type": "command",
							"command": "merge-conflict.accept.selection"
						},
						{
							"key": "B",
							"name": "Accept all both",
							"icon": "arrow-both",
							"type": "command",
							"command": "merge-conflict.accept.all-both"
						},
						{
							"key": "C",
							"name": "Accept all current",
							"icon": "arrow-right",
							"type": "command",
							"command": "merge-conflict.accept.all-current"
						},
						{
							"key": "I",
							"name": "Accept all incoming",
							"icon": "arrow-left",
							"type": "command",
							"command": "merge-conflict.accept.all-incoming"
						},
						{
							"key": "N",
							"name": "Previous Conflict",
							"icon": "arrow-up",
							"type": "command",
							"command": "merge-conflict.previous"
						}
					]
				}
			]
		},
		{
			"key": "z",
			"name": "+Zoom/Fold",
			"icon": "zoom-in",
			"type": "bindings",
			"bindings": [
				{
					"key": "f",
					"name": "+Frame",
					"icon": "window",
					"type": "transient",
					"bindings": [
						{
							"key": "+",
							"name": "Zoom in",
							"icon": "zoom-in",
							"type": "command",
							"command": "workbench.action.zoomIn"
						},
						{
							"key": "-",
							"name": "Zoom out",
							"icon": "zoom-out",
							"type": "command",
							"command": "workbench.action.zoomOut"
						},
						{
							"key": "0",
							"name": "Reset zoom",
							"icon": "search",
							"type": "command",
							"command": "workbench.action.zoomReset"
						},
						{
							"key": "=",
							"name": "Zoom in",
							"icon": "zoom-in",
							"type": "command",
							"command": "workbench.action.zoomIn"
						},
						{
							"key": "j",
							"name": "Zoom out",
							"icon": "zoom-out",
							"type": "command",
							"command": "workbench.action.zoomOut"
						},
						{
							"key": "k",
							"name": "Zoom in",
							"icon": "zoom-in",
							"type": "command",
							"command": "workbench.action.zoomIn"
						}
					]
				},
				{
					"key": "i",
					"name": "+Image preview",
					"icon": "eye",
					"type": "transient",
					"bindings": [
						{
							"key": "+",
							"name": "Zoom in",
							"icon": "zoom-in",
							"type": "command",
							"command": "imagePreview.zoomIn"
						},
						{
							"key": "-",
							"name": "Zoom out",
							"icon": "zoom-out",
							"type": "command",
							"command": "imagePreview.zoomOut"
						},
						{
							"key": "=",
							"name": "Zoom in",
							"icon": "zoom-in",
							"type": "command",
							"command": "imagePreview.zoomIn"
						}
					]
				},
				{
					"key": "x",
					"name": "+Font",
					"icon": "case-sensitive",
					"type": "transient",
					"bindings": [
						{
							"key": "+",
							"name": "Zoom in",
							"icon": "zoom-in",
							"type": "command",
							"command": "editor.action.fontZoomIn"
						},
						{
							"key": "-",
							"name": "Zoom out",
							"icon": "zoom-out",
							"type": "command",
							"command": "editor.action.fontZoomOut"
						},
						{
							"key": "0",
							"name": "Reset zoom",
							"icon": "search",
							"type": "command",
							"command": "editor.action.fontZoomReset"
						},
						{
							"key": "=",
							"name": "Zoom in",
							"icon": "zoom-in",
							"type": "command",
							"command": "editor.action.fontZoomIn"
						},
						{
							"key": "j",
							"name": "Zoom out",
							"icon": "zoom-out",
							"type": "command",
							"command": "editor.action.fontZoomOut"
						},
						{
							"key": "k",
							"name": "Zoom in",
							"icon": "zoom-in",
							"type": "command",
							"command": "editor.action.fontZoomIn"
						}
					]
				},
				{
					"key": ".",
					"name": "+Fold",
					"icon": "fold",
					"type": "bindings",
					"bindings": [
						{
							"key": "a",
							"name": "Toggle: around a point",
							"icon": "selection",
							"type": "command",
							"command": "editor.toggleFold"
						},
						{
							"key": "b",
							"name": "Close: all block comments",
							"icon": "fold",
							"type": "command",
							"command": "editor.foldAllBlockComments"
						},
						{
							"key": "c",
							"name": "Close: at a point",
							"icon": "fold",
							"type": "command",
							"command": "editor.fold"
						},
						{
							"key": "g",
							"name": "Close: all regions",
							"icon": "fold",
							"type": "command",
							"command": "editor.foldAllMarkerRegions"
						},
						{
							"key": "m",
							"name": "Close: all",
							"icon": "fold",
							"type": "command",
							"command": "editor.foldAll"
						},
						{
							"key": "o",
							"name": "Open: at a point",
							"icon": "unfold",
							"type": "command",
							"command": "editor.unfold"
						},
						{
							"key": "r",
							"name": "Open: all",
							"icon": "unfold",
							"type": "command",
							"command": "editor.unfoldAll"
						},
						{
							"key": "G",
							"name": "Open: all regions",
							"icon": "unfold",
							"type": "command",
							"command": "editor.unfoldAllMarkerRegions"
						},
						{
							"key": "O",
							"name": "Open: recursively",
							"icon": "unfold",
							"type": "command",
							"command": "editor.unfoldRecursively"
						}
					]
				}
			]
		},
		{
			"key": "D",
			"name": "+Diff/Compare",
			"icon": "diff",
			"type": "bindings",
			"bindings": [
				{
					"key": "c",
					"name": "Compare active file with clipboard",
					"icon": "clippy",
					"type": "command",
					"command": "workbench.files.action.compareWithClipboard"
				},
				{
					"key": "m",
					"name": "Compare current merge conflict",
					"icon": "git-merge",
					"type": "command",
					"command": "merge-conflict.compare"
				},
				{
					"key": "s",
					"name": "Compare active file with saved",
					"icon": "save-as",
					"type": "command",
					"command": "workbench.files.action.compareWithSaved"
				},
				{
					"key": "w",
					"name": "Toggle ignore trim whitespace",
					"icon": "whitespace",
					"type": "command",
					"command": "toggle.diff.ignoreTrimWhitespace"
				},
				{
					"key": "D",
					"name": "+Compare active file with",
					"icon": "diff",
					"type": "command",
					"command": "workbench.files.action.compareFileWith"
				}
			]
		},
		{
			"key": "F",
			"name": "+Frame",
			"icon": "window",
			"type": "bindings",
			"bindings": [
				{
					"key": "n",
					"name": "Duplicate workspace in new frame",
					"icon": "window",
					"type": "command",
					"command": "workbench.action.duplicateWorkspaceInNewWindow"
				},
				{
					"key": "o",
					"name": "Switch frame",
					"icon": "multiple-windows",
					"type": "command",
					"command": "workbench.action.quickSwitchWindow"
				},
				{
					"key": "N",
					"name": "Open new empty frame",
					"icon": "empty-window",
					"type": "command",
					"command": "workbench.action.newWindow"
				}
			]
		},
		{
			"key": "S",
			"name": "+Show",
			"icon": "info",
			"type": "bindings",
			"bindings": [
				{
					"key": "d",
					"name": "Show debug console",
					"icon": "debug-console",
					"type": "command",
					"command": "workbench.debug.action.toggleRepl"
				},
				{
					"key": "e",
					"name": "Show explorer",
					"icon": "list-tree",
					"type": "command",
					"command": "workbench.view.explorer"
				},
				{
					"key": "g",
					"name": "Show source control",
					"icon": "source-control",
					"type": "command",
					"command": "workbench.view.scm"
				},
				{
					"key": "n",
					"name": "Show notification",
					"icon": "comment",
					"type": "command",
					"command": "notifications.toggleList"
				},
				{
					"key": "o",
					"name": "Show output",
					"icon": "output",
					"type": "command",
					"command": "workbench.action.output.toggleOutput"
				},
				{
					"key": "p",
					"name": "Show problem",
					"icon": "error",
					"type": "command",
					"command": "workbench.actions.view.problems"
				},
				{
					"key": "r",
					"name": "Show remote explorer",
					"icon": "remote-explorer",
					"type": "command",
					"command": "workbench.view.remote"
				},
				{
					"key": "s",
					"name": "Show search",
					"icon": "search",
					"type": "command",
					"command": "workbench.view.search"
				},
				{
					"key": "t",
					"name": "Show test",
					"icon": "beaker",
					"type": "command",
					"command": "workbench.view.extension.test"
				},
				{
					"key": "x",
					"name": "Show extensions",
					"icon": "extensions",
					"type": "command",
					"command": "workbench.view.extensions"
				}
			]
		},
		{
			"key": "T",
			"name": "+UI toggles",
			"icon": "tools",
			"type": "bindings",
			"bindings": [
				{
					"key": "b",
					"name": "Toggle side bar visibility",
					"icon": "split-horizontal",
					"type": "command",
					"command": "workbench.action.toggleSidebarVisibility"
				},
				{
					"key": "c",
					"name": "Toggle centered layout",
					"icon": "list-flat",
					"type": "command",
					"command": "workbench.action.toggleCenteredLayout"
				},
				{
					"key": "i",
					"name": "Select icon theme",
					"icon": "symbol-misc",
					"type": "command",
					"command": "workbench.action.selectIconTheme"
				},
				{
					"key": "j",
					"name": "Toggle panel visibility",
					"icon": "output",
					"type": "command",
					"command": "workbench.action.togglePanel"
				},
				{
					"key": "m",
					"name": "Toggle maximized panel",
					"icon": "chevron-up",
					"type": "command",
					"command": "workbench.action.toggleMaximizedPanel"
				},
				{
					"key": "s",
					"name": "Select theme",
					"icon": "paintcan",
					"type": "command",
					"command": "workbench.action.selectTheme"
				},
				{
					"key": "t",
					"name": "Toggle tool/activity bar visibility",
					"icon": "tools",
					"type": "command",
					"command": "workbench.action.toggleActivityBarVisibility"
				},
				{
					"key": "z",
					"name": "Toggle zen mode",
					"icon": "eye",
					"type": "command",
					"command": "workbench.action.toggleZenMode"
				},
				{
					"key": "F",
					"name": "Toggle full screen",
					"icon": "screen-full",
					"type": "command",
					"command": "workbench.action.toggleFullScreen"
				},
				{
					"key": "M",
					"name": "Toggle minimap",
					"icon": "symbol-ruler",
					"type": "command",
					"command": "editor.action.toggleMinimap"
				},
				{
					"key": "T",
					"name": "Toggle tab visibility",
					"icon": "files",
					"type": "command",
					"command": "workbench.action.toggleTabsVisibility"
				}
			]
		}
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
        "command": "vspacecode.space",
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