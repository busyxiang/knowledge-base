### Branch Management
#### Create and Switch Branches
```bash
# Create and switch to a new branch
git checkout -b <branch>

# Switch to an existing branch
git switch <branch>
```
#### Delete Branches
```bash
# Delete a local branch (safe, checks for unmerged changes)
git branch -d <branch>
```
#### Push and Pull Branches
```bash
# Push to a different branch
git push origin <source>:<target>

# Pull a remote branch without switching
git fetch origin <remote-branch>:<local-branch>
```
### Undoing Changes
#### Discard Uncommitted Changes
```bash
# Discard all uncommitted changes (staged and unstaged)
git reset --hard

# Remove untracked files and directories
git clean -fxd
```
#### Reset Commits
```bash
# Soft reset (keeps changes staged)
git reset --soft HEAD~1

# Mixed reset (unstages changes but keeps them)
git reset --mixed HEAD~1

# Hard reset (discards all changes)
git reset --hard HEAD~1

# Reset to match remote branch
git reset --hard origin/master
```
### Tags
```bash
# Force update tags
git fetch --tags --force

# Resolve conflicting tags
git pull --tags -f
```
### Submodules
```bash
# Update all submodules recursively
git submodule update --recursive --remote
```
### Rebasing and Squashing
```bash
# Rebase current branch onto another branch (e.g., main)
git checkout new-feature
git rebase main

# Squash the last X commits interactively
git rebase -i HEAD~[x]
```
> [!info]
> For interactive rebase, the editor will open with a file like this
> ```bash
> pick fda59df commit 1
> pick x536897 commit 2
> pick c01a668 commit 3
> ```
> To transform all these commits into a single one, change the file to this
> ```bash
> pick fda59df commit 1
> squash x536897 commit 2
> squash c01a668 commit 3
> ```
> Then `:wq` save the changes and quit the editor
### File History
```bash
# View commit history for a specific file
git log -- [file_path]
```
### Aliases
#### Add Aliases via CLI
```bash
git config --global alias.fa "fetch --all --prune"
```
#### Edit Aliases Manually
```bash
git config --global -e
```
Add to the file:
```vim
[alias]
    fa = fetch --all --prune
    st = status
    co = checkout
    br = branch
```
### Additional Useful Commands
```bash
# Show a specific commit by hash
git show [HASH]
```
## Tools
#### Check Repo Size
- [git-sizer](https://github.com/github/git-sizer)
- https://www.jonathancreamer.com/how-we-shrunk-our-git-repo-size-by-94-percent/