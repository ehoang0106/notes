
Install packages:

```bash
sudo pacman -S --needed fcitx5 fcitx5-unikey fcitx5-configtool fcitx5-gtk fcitx5-qt
```

add the config to `~/.config/hypr/hyprland.conf`

```yaml
# --- Input Method (Fcitx5) ---
env = GTK_IM_MODULE,fcitx
env = QT_IM_MODULE,fcitx
env = XMODIFIERS,@im=fcitx
```

add 1 more line to a same file to auto start fcitx when log in:

```bash
exec-once = fcitx5 -d
```

to configure fcitx5 run command:

```bash
fcitx5-configtool
```

Use `control` + `space` to switch input method
