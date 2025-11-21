with `echo -e`:

```bash
echo -e "Hello\nWorld"
```

output: 

```bash
Hello
World
```

without `-e`:

```bash
echo "Hello\nWorld"
```

output:

```bash
Hello\nWorld
```

```bash
#clone the git repo contains waybar config files and kitty config files
GITHUB_REPO_URL="git@github.com:ehoang0105/omarchy-config.git"
cd $HOME
mkdir omarchy-config-script && cd omarchy-config-script
git clone $GITHUB_REPO_URL
cd omarchy-config
cd waybar
cp config.jsonc $WAYBAR_CONFIG_DIR/config.jsonc
cp style.css $WAYBAR_CONFIG_DIR/style.css


```