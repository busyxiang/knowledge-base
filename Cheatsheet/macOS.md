## Killing Localhost Processes

To terminate a process running on a specific port (e.g., `localhost:8000`):
1. Find the Process ID (PID):
```bash
sudo lsof -i :8000
```
2. Kill the process using the PID:
```bash
kill -9 <PID>
```
## Homebrew Setup
### Brewfile Management
#### Installation
- Install from default Brewfile (`~/Brewfile`):
```bash
brew bundle install
```
- Install from a specific Brewfile:
```bash
brew bundle --file=~/.private/Brewfile
```
#### Creating a Brewfile
Generate a Brewfile from your current installations:
```bash
brew bundle dump
```
### My brewfile
```ruby
# command-line utilities
brew "git"
brew "lazygit"
brew "nvm"
brew "zsh"
brew "zsh-autosuggestions"

# apps
cask "iterm2"
cask "raycast"
cask "sourcetree"
cask "spotify"
cask "visual-studio-code"
```
---
## iTerm2 Setup
### Recommended Plugins
- **[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)**
	Provides fish-like autosuggestions for Zsh.