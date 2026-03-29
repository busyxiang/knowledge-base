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
| `Ctrl+o`    | Jump back in jump list                      |
| `Ctrl+i`    | Jump forward in jump list                   |

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
