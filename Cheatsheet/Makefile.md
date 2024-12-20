## Variables
### Define and Use Variables

```makefile
NAME = value

print:
	echo $(NAME)
```
### Evaluate at Runtime

```makefile
variable:
	$(eval FOO := bar) # Sets FOO dynamically
	echo $(FOO)
```
### Environment Variables

```makefile
print-env:
	echo $$USER # Escaped `$` to access shell vars
```
## Strings and Text Manipulation
### Replace Text in a File
```makefile
replace-text:
    sed -i '' -e 's/{OLD_TEXT}/$(NEW_TEXT)/g' ./file.txt
```
- `-i ''`: Edit file in-place (macOS syntax; use `-i` alone on Linux).
## User Input
### Interactive Input
```makefile
greet:
    @read -p "First name: " first; \
    read -p "Last name: " last; \
    echo "Hello, $$first $$last!"
```
- `@`: Suppresses command echo.
- `\`: Continues the command on the next line.
- `-p`: Displays a prompt.
## Conditional Logic
```makefile
deploy:
    @if [ -f "config.env" ]; then \
        echo "Config found"; \
    else \
        echo "Error: Missing config.env"; exit 1; \
    fi
```