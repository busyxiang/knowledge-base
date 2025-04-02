# Variables
```makefile
variable:
	$(eval FOO := bar)
	echo $(FOO)
```
# String
## Replace text in a file
```makefile
replace-text:
	sed -i '' -e 's/{TEXT_TO_REPLACE}/$(REPLACE_TEXT)/g' ./test-file.txt
```
# Input
```makefile
greet:
	@read -p "What's your first name? " firstName; \
	read -p "What's your last name? " lastName; \
	echo "Hello, $$firstName $$lastName! Welcome to the Makefile."
```
- `\` means multiline command
- `@` symbol suppress the command echo in the output. When use at the beginning of a line, it will affects the entire logical line including all continuations with `\`