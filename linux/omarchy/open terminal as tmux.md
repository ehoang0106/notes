
```bash
nvim ~/.bashrc
```

add:

```bash
if command -v tmux >/dev/null 2>&1; then
    [ -z "$TMUX" ] && tmux
fi
```
