## Process Management

### Kill a Process by Port

```bash
# Find the PID on a specific port
sudo lsof -i :8000

# Kill it
kill -9 <PID>

# One-liner
sudo kill -9 $(sudo lsof -t -i:8000)
```

---

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

---

## Terminal Navigation Shortcuts

| Shortcut   | Description                   |
| ---------- | ----------------------------- |
| `Ctrl + A` | Jump to start of the line     |
| `Ctrl + E` | Jump to end of the line       |
| `Ctrl + R` | Search command history        |
| `Ctrl + U` | Clear before cursor           |
| `Ctrl + K` | Clear after cursor            |
| `cd -`     | Go back to previous directory |

---

## Command History

| Command                      | Description                  |
| ---------------------------- | ---------------------------- |
| `!!`                         | Repeat the last command      |
| `history`                    | View command history         |
| `history \| grep [keyword]`  | Search history for a keyword |

---

## Searching and Filtering Text

```bash
# Basic pattern search
grep "error" log.txt

# Case-insensitive search
grep -i "warning" log.txt

# Recursive search in directories
grep -r "pattern" /path/to/directory
```

---

## String Manipulation

```bash
# Trim a string
str='This is an example sentence'
echo "${str:0:15}" # Output: "This is an exam"
```

---

## File Manipulation

```bash
# Combine multiple text files into one
cat file1 file2 file3 > combined.txt
cat *.txt > combined.txt

# Copy files with visual progress
rsync --progress file1.txt /opt
```

---

## Certificate Conversion (OpenSSL)

```bash
# Convert .cer (DER) to .pem
openssl x509 -in cert.cer -inform DER -out cert.pem -outform PEM

# Convert .crt (PEM) to .pem
openssl x509 -in cert.crt -inform PEM -out cert.pem -outform PEM
```

---

## Alias Management

```bash
# Create a permanent alias (add to ~/.bash_aliases or ~/.bashrc)
alias <name>='<command>'

# List all aliases
alias

# Find alias source
which [alias]
```

---

## Command Chaining Operators

| Operator | Description                                | Example                              |
| -------- | ------------------------------------------ | ------------------------------------ |
| `&`      | Run command in background                  | `ping google.com &`                  |
| `;`      | Run commands sequentially                  | `apt update; apt upgrade`            |
| `&&`     | Run next only if previous succeeds         | `ping google.com && ls`              |
| `\|\|`   | Run next only if previous fails            | `apt update \|\| echo "Failed"`     |
| `!`      | Exclude pattern                            | `rm -r !(*.html)`                    |
| `{}`     | Command grouping                           | `[ -d bin ] \|\| { mkdir bin; }`    |
| `()`     | Precedence grouping                        | `(cmd1 && cmd2) \|\| (cmd3 && cmd4)` |
| `\`      | Line continuation                          | Multi-line commands                  |

---

## SSH Port Forwarding

SSH tunneling allows you to forward ports between local and remote machines.

```bash
# Local port forwarding: access remote port via localhost
ssh -L [local_port]:localhost:[remote_port] user@remote_host

# Example: Forward remote PostgreSQL
ssh -L 5432:localhost:5432 user@db-server.com

# Forward through a jump server
ssh -L 9000:other-server:80 user@jump-server.com

# Remote port forwarding: expose local port to remote
ssh -R 8080:localhost:3000 user@server.com

# Dynamic port forwarding (SOCKS proxy)
ssh -D 1080 user@server.com

# Background connection (no shell)
ssh -fN -L 8080:localhost:80 user@server.com

# Multiple port forwards
ssh -L 8080:localhost:80 -L 3306:localhost:3306 user@server.com

# With specific SSH key
ssh -i ~/.ssh/my_key -L 8080:localhost:80 user@server.com
```
