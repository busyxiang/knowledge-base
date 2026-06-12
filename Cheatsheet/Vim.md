## Modes
| Key | Description         |
| --- | ------------------- |
| i   | insert              |
| :   | command             |
| v   | visual              |
| esc | exit to normal mode |

## Navigation (Normal Mode)
| Command       | Action                                      |
| ------------- | ------------------------------------------- |
| `h j k l`     | Left / down / up / right                   |
| `w`           | Jump to start of next word                  |
| `b`           | Jump to start of previous word              |
| `e`           | Jump to end of word                         |
| `0`           | Jump to start of line                       |
| `^`           | Jump to first non-blank character of line   |
| `$`           | Jump to end of line                         |
| `gg`          | Go to first line of file                    |
| `G`           | Go to last line of file                     |
| `{n}G`        | Go to line n (e.g., `42G`)                  |
| `:n`          | Go to line n (e.g., `:42`)                  |
| `Ctrl+u`      | Move up half a page                         |
| `Ctrl+d`      | Move down half a page                       |
| `Ctrl+b`      | Move up full page                           |
| `Ctrl+f`      | Move down full page                         |
| `zz`          | Center current line on screen               |
| `zt`          | Scroll current line to top                  |
| `zb`          | Scroll current line to bottom               |

## Jumping
| Command     | Action                                      |
| ----------- | ------------------------------------------- |
| `%`         | Jump to matching bracket `()` `[]` `{}`    |
| `*`         | Search word under cursor (forward)          |
| `#`         | Search word under cursor (backward)         |
| `''`        | Jump back to last position                  |
| `Ctrl+o`    | Backtrack to previous location (jump list)  |
| `Ctrl+i`    | Move forward to next location (jump list)   |

## Code Navigation (LSP)
Native `gd`/`gD` work in plain Vim (search local/global declaration). `gr`, `gi`, `gy` are standard Neovim LSP bindings (Nvim 0.10+ defaults; otherwise mapped to `vim.lsp.buf.*`).

| Command | Action                                              |
| ------- | --------------------------------------------------- |
| `gd`    | Go to definition of symbol under cursor             |
| `gD`    | Go to declaration (e.g., header/extern declaration) |
| `gr`    | List references to symbol under cursor              |
| `gi`    | Go to implementation                                |
| `gy`    | Go to type definition                               |

## Folding
Set a fold method first, e.g. `:set foldmethod=indent` (or `syntax`, `manual`, `marker`). `za` toggles; uppercase variants act recursively on nested folds.

| Command | Action                                       |
| ------- | -------------------------------------------- |
| `zf{motion}` | Create fold over a motion (manual method) |
| `za`    | Toggle fold under cursor                     |
| `zo`    | Open fold under cursor                       |
| `zc`    | Close fold under cursor                      |
| `zO`    | Open fold recursively                        |
| `zC`    | Close fold recursively                       |
| `zR`    | Open all folds in file                       |
| `zM`    | Close all folds in file                      |
| `zd`    | Delete fold under cursor                     |
| `zj`    | Jump to next fold                            |
| `zk`    | Jump to previous fold                        |

## Search
| Command      | Action                      |
| ------------ | --------------------------- |
| `/pattern`   | Search forward              |
| `?pattern`   | Search backward             |
| `n`          | Next match                  |
| `N`          | Previous match              |
| `:noh`       | Clear search highlight      |

## Marks
| Command  | Action           |
| -------- | ---------------- |
| `ma`     | Set mark `a`     |
| `` `a `` | Jump to mark `a` |

## Splits & Windows
| Command            | Action                      |
| ------------------ | --------------------------- |
| `Ctrl+w s`         | Horizontal split            |
| `Ctrl+w v`         | Vertical split              |
| `Ctrl+w h/j/k/l`   | Move between splits         |
| `Ctrl+w q`         | Close split                 |

## Buffers
| Command | Action          |
| ------- | --------------- |
| `:bn`   | Next buffer     |
| `:bp`   | Previous buffer |
| `:bd`   | Delete buffer   |

## File Operations (Command Mode)
| Command | Description              |
| ------- | ------------------------ |
| `:q`    | Quit                     |
| `:q!`   | Quit and discard changes |
| `:w`    | Save file                |
| `:wq`   | Save and quit            |

## Commenting
`gc` is the Neovim 0.10+ built-in comment toggle (also provided by `tpope/vim-commentary` / `numToStr/Comment.nvim`). Plain Vim has no native toggle — use the visual-block approach.

| Command      | Action                                          |
| ------------ | ----------------------------------------------- |
| `gcc`        | Toggle comment on current line                  |
| `gc{motion}` | Toggle comment over a motion (e.g., `gc3j`)     |
| `gc` (visual)| Toggle comment on selected lines                |
| `gcap`       | Toggle comment on a paragraph                   |

### Without a plugin (manual)
| Command                       | Action                                  |
| ----------------------------- | --------------------------------------- |
| `Ctrl+v`, select, `I // esc`  | Block-insert `//` to comment lines      |
| `Ctrl+v`, select column, `x`  | Delete the comment chars to uncomment   |
| `:s/^/# /` (visual range)     | Prefix selected lines with `# `         |
| `:s/^# //` (visual range)     | Remove leading `# ` from selected lines |

## Yank / Copy
Append `+` to a yank to copy into the system clipboard instead of the unnamed register (needs a clipboard-enabled build — check with `vim --version | grep clipboard`).

| Command   | Action                                       |
| --------- | -------------------------------------------- |
| `yy`      | Yank current line                            |
| `y{motion}`| Yank over a motion (e.g., `y3j`)            |
| `ggVGy`   | Yank entire file (unnamed register)          |
| `:%y`     | Yank entire file (command mode)              |
| `gg"+yG`  | Yank entire file to system clipboard         |
| `:%y+`    | Yank entire file to system clipboard         |
| `p`       | Paste after cursor (linewise: line below)    |
| `P`       | Paste before cursor (linewise: line above)   |
| `"+p`     | Paste from system clipboard                  |
| `:put`    | Paste linewise below current line            |
| `yyp`     | Duplicate current line below                 |
| `yyP`     | Duplicate current line above                 |
| `:t.`     | Duplicate current line below (range-capable) |

No default shortcut for line duplication (unlike VS Code's `Shift+Alt+↓/↑`) — map it yourself, e.g. `nnoremap <A-S-Down> yyp` (terminal may not forward Alt/Shift+arrow; a `<leader>` mapping is more reliable).

## Registers
| Command                   | Description                               |
| ------------------------- | ----------------------------------------- |
| `:let @+ = expand("%:t")` | Copy current filename to system clipboard |
| `:let @+ = expand("%.")`  | Copy relative path to system clipboard    |
| `:let @+ = expand("%:p")` | Copy absolute path to system clipboard    |
