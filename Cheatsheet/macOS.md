## Clipboard Operations

```bash
# Copy file contents to clipboard
cat file_path | pbcopy

# Copy command output to clipboard
echo "Hello World" | pbcopy

# Paste clipboard contents to terminal
pbpaste
```

---

## Package Management

### Homebrew Setup

#### Brewfile Management

**Installation**

```bash
# Install from default Brewfile (~/Brewfile)
brew bundle install

# Install from a specific Brewfile location
brew bundle --file=~/.private/Brewfile

# Verbose installation with output
brew bundle install --verbose
```

**Creating and Managing Brewfiles**

```bash
# Generate a Brewfile from your current installations
brew bundle dump

# Generate and overwrite existing Brewfile
brew bundle dump --force

# Check what would be installed/uninstalled
brew bundle check
```

#### My Essential Brewfile

```ruby
# Command-line utilities
brew "git"           # Version control system
brew "lazygit"       # Simple terminal UI for git commands
brew "nvm"           # Node Version Manager
brew "zsh"           # Z shell
brew "zsh-autosuggestions"  # Fish-like autosuggestions for zsh

# Applications
cask "iterm2"               # Better terminal emulator
cask "raycast"              # Spotlight replacement with superpowers
cask "sourcetree"           # Git GUI client
cask "spotify"              # Music streaming
cask "visual-studio-code"   # Code editor
```

---

## Terminal Setup

### iTerm2 Configuration

#### Recommended Plugins

**[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)**

- Provides fish-like autosuggestions for Zsh based on command history
- Installation via Homebrew: `brew install zsh-autosuggestions`
- Add to ~/.zshrc: `source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh`

**Additional useful plugins to consider:**

- **zsh-syntax-highlighting**: Highlights commands as you type
- **Oh My Zsh**: Framework for managing Zsh configuration
