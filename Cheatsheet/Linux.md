## File and Directory Operations
| Command               | Description                                 |
| --------------------- | ------------------------------------------- |
| `ls`                  | List all folders and files                  |
| `ls -l`               | Long format (detailed information)          |
| `ls -a`               | Show all files, including hidden files      |
| `mkdir [folder-name]` | Create a new folder                         |
| `rm [file_path]`      | Delete a file                               |
| `rmdir [folder_path]` | Delete an empty folder                      |
| `rm -rf [path]`       | Force delete everything (use with caution!) |
## Terminal Navigation Shortcuts

| Shortcut   | Description                   |
| ---------- | ----------------------------- |
| `Ctrl + A` | Jump to start of the line     |
| `Ctrl + E` | Jump to end of the line       |
| `Ctrl + R` | Search command history        |
| `Ctrl + U` | Clear before cursor           |
| `Ctrl + K` | Clear after cursor            |
| `cd -`     | Go back to previous directory |
## Command History
| Command                     | Description                  |
| --------------------------- | ---------------------------- |
| `!!`                        | Repeat the last command      |
| `history`                   | View command history         |
| `history \| grep [keyword]` | Search history for a keyword |
## Searching and Filtering Text
```bash
# Basic pattern search
grep "error" log.txt

# Case-insensitive search
grep -i "warning" log.txt

# Recursive search in directories
grep -r "pattern" /path/to/directory
```
## String Manipulation
```bash
# Trim a string
str='This is an example sentence'
echo "${str:0:15}" # Output: "This is an exam"
```
## File Manipulation
```bash
# Combine multiple text files into one file
cat file1 file2 file3 file4 > combined.txt
cat *.txt > combined.txt
cat ./**/*.txt > combined.txt
cat ./**/sample.txt > combined.txt

# Copy files with visual progress (real-time)
rsyc --progress file1.text /opt
```
## Alias Management
```bash
# Create a permanent alias (add to ~/.bash_aliases or ~/.bashrc)
alias <name>='<command>'

# List all aliases
alias

# Find alias source
which [alias]
```
## Command Chaining Operators
| Operator | Description                                | Example                                                        |
| -------- | ------------------------------------------ | -------------------------------------------------------------- |
| `&`      | Run command in background                  | `ping google.com &`<br><br>`ping google.com & ping google.com` |
| `;`      | Run commands sequentially                  | `apt update; apt upgrade`                                      |
| `&&`     | Run next command only if previous succeeds | `ping google.com && ls`                                        |
| \|\|     | Run next command only if previous fails    | apt update \|\| echo "Failed"`                                 |
| `!`      | Exclude pattern                            | `rm -r !(*.html)`                                              |
| `{}`     | Command grouping                           | [ -d bin ] \|\| { echo "Creating bin"; mkdir bin; }            |
| `()`     | Precedence grouping                        | (cmd1 && cmd2) \|\| (cmd3 && cmd4)                             |
| `\`      | Line continuation                          | `cmd1\cmd2`                                                    |

