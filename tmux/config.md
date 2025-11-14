install plug-in manager:

```
https://github.com/tmux-plugins/tpm
```

then

cd to `~/.config/lua/nvim/plugins/`

create a file name `nvim-tmux-navigator.lua`

```lua
return {
  "christoomey/vim-tmux-navigator",
  cmd = {
    "TmuxNavigateLeft",
    "TmuxNavigateDown",
    "TmuxNavigateUp",
    "TmuxNavigateRight",
    "TmuxNavigatePrevious",
    "TmuxNavigatorProcessList",
  },
  keys = {
    { "<c-h>", "<cmd><C-U>TmuxNavigateLeft<cr>" },
    { "<c-j>", "<cmd><C-U>TmuxNavigateDown<cr>" },
    { "<c-k>", "<cmd><C-U>TmuxNavigateUp<cr>" },
    { "<c-l>", "<cmd><C-U>TmuxNavigateRight<cr>" },
    { "<c-\\>", "<cmd><C-U>TmuxNavigatePrevious<cr>" },
  },
}
```



create/edit `~/tmux.conf` file:

```bash
unbind r
bind r source-file ~/.tmux.conf

set -g prefix C-s

set -g mouse on

bind-key h select-pane -L
bind-key j select-pane -D
bind-key k select-pane -U
bind-key l select-pane -R
bind-key v split-window -v -c '#{pane_current_path}'
bind-key h split-window -h -c '#{pane_current_path}'

set-option -g status-position top

set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'christoomey/vim-tmux-navigator'
set -g @vim_navigator_mapping_left "C-Left C-h"  # use C-h and C-Left
set -g @vim_navigator_mapping_right "C-Right C-l"
set -g @vim_navigator_mapping_up "C-k"
set -g @vim_navigator_mapping_down "C-j"
set -g @tmux-everforest 'dark-medium'

run '~/.tmux/plugins/tpm/tpm'

```

then go to tmux to install plugin

```bash
ctrl + S + I
```

edit `~/.config/nvim/lua/config/options.lua`

```lua
vim.opt.number = true
vim.opt.relativenumber = true
```

edit `~/.config/nvim/lua/config/keymaps.lua`

```lua
vim.keymap.set({ "n", "v" }, "<leader>v", ":vnew<CR>")
vim.keymap.set({ "n", "v" }, "<leader>h", ":new<CR>")
```
