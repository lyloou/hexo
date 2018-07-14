- [Tmux 快捷键 & 速查表](https://gist.github.com/ryerh/14b7c24dfd623ef8edc7)

```conf
bind r source-file ~/.tmux.conf \; display-message "Config reloaded"

bind '"' split-window -c '#{pane_current_path}'
bind '%' split-window -h -c '#{pane_current_path}'

bind Escape copy-mode
bind-key -Tcopy-mode-vi 'v' send -X begin-selection
bind-key -Tcopy-mode-vi 'y' send -X copy-selection
unbind p
bind p pasteb
setw -g mode-keys vi      # Vi风格选择文本

set -g mouse on # 启用鼠标

########### myself ##########
# select panel
bind k selectp -U
bind j selectp -D
bind h selectp -L
bind l selectp -R

set-option -g default-shell /bin/zsh
```

- [How do I rename a session in tmux? - Super User](https://superuser.com/questions/428016/how-do-i-rename-a-session-in-tmux)
`Ctrl` + `B`, `$`
