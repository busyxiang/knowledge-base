# Kill localhost process
For example, if the port is `localhost:8000`. run
```bash
sudo lsof -i :8000

```
Then run
```bash
kill -9 <PID>
```
# Homebrew Setup
## Brewfile
### Install
```bash
# Looks for "~/Brewfile" and installs its contents
brew bundle install

# Install specific brewfile
brew bundle --file=~/.private/Brewfile
```
### Create
dump a Brewfile of your current brew/cask/mas
```bash
brew bundle dump
```
### My brewfile
```ruby

```
# ITerm2 Setup
## Plugins
- **[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)**