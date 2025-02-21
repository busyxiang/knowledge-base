## Create new branch and switch to it
```bash
git checkout -b <branch>
```
## Discard existing files uncommitted changes
```bash
git reset --hard
```
## Remove new and uncommitted files
```bash
git clean -fxd
```
## Switch local branch
```bash
git switch <branch>
```
## Delete Local Branch
```bash
git branch -d <branch>
```
## Push to another branch
```bash
git push origin <source>:<target>
```
## Resolve conflicting tags
```bash
git pull --tags -f
```
## Pull another branch without switching
```bash
git fetch origin <remote-branch>:<local-branch>
```
## Update submodules
```bash
git submodule update --recursive --remote
```
## Rebase
Lets say you are working on `new-feature` branch and want to integrate latest changes from `main` into the `new-feature` branch
```bash
git checkout new-feature
git rebase main
```
## Force Update Tags
```bash
git fetch --tags --force
```
## Find Commit By Hash
```bash
git show [HASH]
```
## Reset Mixed
```bash
git reset --mixed head~1
```
## Squash the Last X Commits
```bash
git rebase -i HEAD~[x]
```
The editor will open with a file like this
```bash
pick fda59df commit 1
pick x536897 commit 2
pick c01a668 commit 3
```
To transform all these commits into a single one, change the file to this
```bash
pick fda59df commit 1
squash x536897 commit 2
squash c01a668 commit 3
```
Then `:wq` save the changes and quit the editor
# Aliases
Open git config file
```bash
git config --global -e
```
Add the following in the file
```vim
[alias]
	fa = fetch --all --prune
```

OR

Using the CLI
```bash
git config --global alias.fa "fetch --all --prune"
```
# Tools
### Check Repo Size
- [git-sizer](https://github.com/github/git-sizer)
- https://www.jonathancreamer.com/how-we-shrunk-our-git-repo-size-by-94-percent/