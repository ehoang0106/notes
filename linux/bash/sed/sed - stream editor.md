if we have a file in `~/.config/uwsm/default` contain:

```bash
# Changes require a restart to take effect.

# Install other terminals via Install > Terminal
export TERMINAL=alacritty

# Use code for VSCode
export EDITOR=nvim

# Use a custom directory for screenshots (remember to make the directory!)
export OMARCHY_SCREENSHOT_DIR="$HOME/Pictures/Screenshots"

# Use a custom directory for screenrecordings (remember to make the directory!)
export OMARCHY_SCREENRECORD_DIR="$HOME/Videos/Screencasts"

```

end want to change the `export TERMINAL=alacritty` to `export TERMINAL=kitty` 

use `sed`:

```bash
#!/bin/bash

# Define the file path
CONFIG_FILE="$HOME/.config/uwsm/config"

# Define the old and new terminal values
OLD_TERMINAL="kitty"
NEW_TERMINAL="alacritty"

# Use sed to replace the line
sed -i "s/export TERMINAL=$OLD_TERMINAL/export TERMINAL=$NEW_TERMINAL/" "$CONFIG_FILE"

echo "Updated terminal setting in $CONFIG_FILE."
echo "Old: export TERMINAL=$OLD_TERMINAL"
echo "New: export TERMINAL=$NEW_TERMINAL"
```

- **`sed -i`**: The **`sed`** (Stream Editor) command is used for simple text transformations on an input stream (a file). The **`-i`** flag tells `sed` to edit the file **in place** (modifying the original file).
    
- **`"s/.../.../"`**: This is the substitution command (`s/`) pattern.
    
    - The first part, **`export TERMINAL=$OLD_TERMINAL`** (which evaluates to `export TERMINAL=kitty`), is the **pattern** to search for.
        
    - The second part, **`export TERMINAL=$NEW_TERMINAL`** (which evaluates to `export TERMINAL=alacritty`), is the **replacement** string.