## Modes
| Key | Description         |
| --- | ------------------- |
| i   | insert              |
| :   | command             |
| v   | visual              |
| esc | exit to normal mode |
## Navigation (Normal Mode)
| Command  | Action                         |
| -------- | ------------------------------ |
| `w`      | Jump to start of next word     |
| `b`      | Jump to start of previous word |
| `0`      | Jump to start of line          |
| `$`      | Jump to end of line            |
| `gg`     | Go to first line of file       |
| `G`      | Go to last line of file        |
| `:n`     | Go to line `n` (e.g., `:42`)   |
| `Ctrl+u` | Move up half a page            |
| `Ctrl+d` | Move down half a page          |
## Search (Normal Mode)

| Command  | Action                                      |
| -------- | ------------------------------------------- |
| `/text`  | Search forward for `text`                   |
| `?text`  | Search backward for `text`                  |
| `n`      | Jump to next match                          |
| `N`      | Jump to previous match                      |
| `*`      | Search forward for word under cursor        |
| `#`      | Search backward for word under cursor       |
| `:noh`   | Clear search highlight                      |

## File Operations (Command Mode)

| Command | Description              |
| ------- | ------------------------ |
| `:q`    | Quit                     |
| `:q!`   | Quit and discard changes |
| `:w`    | Save file                |
| `:wq`   | Save and quit            |
