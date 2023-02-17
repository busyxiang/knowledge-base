# Command
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
## Push to another branch
```bash
git push origin <source>:<target>
```
## Resolve conflicting tags
```bash
git pull --tags -f
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