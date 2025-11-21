check if git is installed:

```bash
if command -v git &> /dev/null; then
	echo "git is installed!"
else
	echo "git is not installed"
```

check if kitty is installed:

```bash
if ! command -v kitty &> /dev/null; then
	echo "kitty is not installed."
else
	echo "kitty is installed!"
```