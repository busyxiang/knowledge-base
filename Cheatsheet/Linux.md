# Command
| Command             | Description                |
| ------------------- | -------------------------- |
| ls                  | List all folders and files |
| mkdir [folder-name] | Create folder              |
| rm [file_path]      | Delete file                |
| rmdir [folder_path] | Delete folder              |
| rm -rf [path]       | Delete everything          |
| alias               | List all alias             |
| which [alias]       | Get alias source           |
# Alias
## Create Permanent Alias
Edit  `~/.bash_aliases` or `~/.bashrc`  file
```bash
alias <name>='<command>'
```
# Command Chaining Operators
## Ampersand (&)
This operator is to make the command run in the background

Run a single command in the background
```bash
ping www.google.com &
```

Run two or multiple commands in the background
```bash
apt update & apt upgrade &
```
## Semi-Colon (;)
This operator makes it possible to run multiple commands in a single go
```bash
apt update ; apt upgrade ; mkdir test
```
## AND (&&)
This operator would execute the second command only if the execution of the first command **SUCCEEDS**
```bash
ping www.google.com && ls
```
## OR (||)
This operator allows to execute second command only if the execution of the first command fails
```bash
apt update || links tecmint.com
```
## NOT (!)
This operator execute all except the condition provided
```bash
rm -r !(*.html)
```
## Command Combination {}
This operator combine two or more commands
```bash
[ -d bin ] || { echo Directory does not exist, creating directory now.; mkdir bin; } && echo Directory exists.
```
## Precedence ()
This operator makes it possible to execute commands in precedence order
```bash
(Command_x1 &&Command_x2) || (Command_x3 && Command_x4)
```
## Concatenation \\
This operator is used to concatenate large commands over several lines.

The below command will open a text file **test(1).txt**.
```bash
nano test\(1\).txt
```