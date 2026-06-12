The **prefix** is `Ctrl+b` by default. Most commands are typed as `prefix` then the key (release prefix first). Commands prefixed with `:` are entered in the tmux command prompt (`prefix :`).

## Sessions
| Command                     | Action                              |
| --------------------------- | ----------------------------------- |
| `tmux`                      | Start a new session                 |
| `tmux new -s [name]`        | Start a named session               |
| `tmux ls`                   | List sessions                       |
| `tmux a` / `tmux attach`    | Attach to last session              |
| `tmux a -t [name]`          | Attach to a named session           |
| `tmux kill-session -t [name]` | Kill a named session              |
| `tmux kill-server`          | Kill all sessions                   |
| `prefix d`                  | Detach from current session         |
| `prefix s`                  | List/switch sessions                |
| `prefix $`                  | Rename current session              |
| `prefix (` / `prefix )`     | Switch to previous / next session   |

## Windows
| Command       | Action                            |
| ------------- | --------------------------------- |
| `prefix c`    | Create a new window               |
| `prefix ,`    | Rename current window             |
| `prefix &`    | Close current window              |
| `prefix n`    | Next window                       |
| `prefix p`    | Previous window                   |
| `prefix [0-9]`| Switch to window by number        |
| `prefix w`    | List windows (interactive)        |
| `prefix f`    | Find window by name               |
| `prefix .`    | Move window to another index      |

## Panes
| Command          | Action                                 |
| ---------------- | -------------------------------------- |
| `prefix %`       | Split pane vertically (left/right)     |
| `prefix "`       | Split pane horizontally (top/bottom)   |
| `prefix ←↑↓→`    | Switch to pane in that direction       |
| `prefix o`       | Cycle to next pane                     |
| `prefix q`       | Show pane numbers (press number to go) |
| `prefix x`       | Close current pane                     |
| `prefix z`       | Toggle pane zoom (fullscreen)          |
| `prefix {` / `}` | Swap pane with previous / next         |
| `prefix space`   | Cycle through pane layouts             |
| `prefix !`       | Convert pane into its own window       |
| `prefix Ctrl+←↑↓→` | Resize pane in that direction        |

## Copy Mode
Enter with `prefix [`, then navigate like Vim (set with `setw -g mode-keys vi`). Exit with `q`.

| Command       | Action                          |
| ------------- | ------------------------------- |
| `prefix [`    | Enter copy mode                 |
| `space`       | Start selection                 |
| `enter`       | Copy selection and exit         |
| `prefix ]`    | Paste copied text               |
| `/` / `?`     | Search forward / backward       |
| `q`           | Quit copy mode                  |

## Misc
| Command     | Action                                  |
| ----------- | --------------------------------------- |
| `prefix ?`  | List all key bindings                   |
| `prefix t`  | Show a large clock                      |
| `prefix :`  | Open the tmux command prompt            |
| `prefix r`  | Reload config (if mapped in `.tmux.conf`) |

## Config
Settings live in `~/.tmux.conf`. Reload a running session with `prefix :` then `source-file ~/.tmux.conf`.

```bash
# Remap prefix to Ctrl+a
unbind C-b
set -g prefix C-a
bind C-a send-prefix

# Use Vim keys in copy mode
setw -g mode-keys vi

# Start windows and panes at 1, not 0
set -g base-index 1
setw -g pane-base-index 1

# Enable mouse support (scroll, select, resize)
set -g mouse on

# Reload config with prefix r
bind r source-file ~/.tmux.conf \; display "Config reloaded"
```

> [!tip]
> Pair tmux with [[Vim]] for a fully keyboard-driven terminal workflow.
