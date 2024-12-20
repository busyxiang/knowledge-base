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