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
## SSH Port Forwarding
SSH port forwarding (SSH tunneling) allows you to forward ports from a remote server to your localhost.

```bash
# Local port forwarding: Forward remote server port to localhost
# Syntax: ssh -L [local_port]:localhost:[remote_port] user@remote_host
ssh -L 8080:localhost:80 user@server.com
# Access remote server's port 80 via localhost:8080

# Example: Forward remote PostgreSQL database
ssh -L 5432:localhost:5432 user@db-server.com
# Connect to database via localhost:5432

# Forward specific remote host through jump server
ssh -L 9000:other-server:80 user@jump-server.com
# Access other-server:80 via localhost:9000

# Remote port forwarding: Expose local port to remote server
ssh -R 8080:localhost:3000 user@server.com
# Remote server can access your localhost:3000 via its port 8080

# Dynamic port forwarding (SOCKS proxy)
ssh -D 1080 user@server.com
# Creates SOCKS proxy on localhost:1080

# Keep connection alive in background
ssh -fN -L 8080:localhost:80 user@server.com
# -f: Run in background, -N: No command execution

# Multiple port forwards
ssh -L 8080:localhost:80 -L 3306:localhost:3306 user@server.com
```

