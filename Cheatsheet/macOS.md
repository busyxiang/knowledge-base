## Process Management

### Killing Localhost Processes

To terminate a process running on a specific port (e.g., `localhost:8000`):

**Method 1: Step by step**

```bash
# 1. Find the Process ID (PID)
sudo lsof -i :8000

# 2. Kill the process using the PID
kill -9 <PID>
```

**Method 2: One-liner**

```bash
# Kill process on port 8000 directly
sudo kill -9 $(sudo lsof -t -i:8000)
```

---

## File Operations

### Certificate Conversion

Convert certificate formats using OpenSSL:

```bash
# Convert .cer/.crt to .pem format
openssl x509 -in [file_name].cer -inform DER -out [file_name].pem -outform PEM

# Alternative for different input formats
openssl x509 -in [file_name].crt -inform PEM -out [file_name].pem -outform PEM
```

### Clipboard Operations

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