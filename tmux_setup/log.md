## install tpm
<https://github.com/tmux-plugins/tpm>

## update .tmux.conf file
```
set-option -g mouse on

set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'tmux-plugins/tmux-prefix-highlight'
set -g @plugin 'sei40kr/tmux-onedark'

run -b '~/.tmux/plugins/tpm/tpm'
```

## download plugins and restart tmux
`Ctrl-B` and `I`
tmux kill-server

### update ~/.tmux/plugins/tmux-onedark remove battery settings and day month order
```
#!/usr/bin/env bash

main() {
  local green='#98c379'
  local dark_green='#00af87'
  local white='#abb2bf'
  local black='#282c34'
  local comment_grey='#5c6370'
  local menu_grey='#3e4452'
  local special_grey='#3b4048'

  tmux set-option -g mode-style 'bg=#3e4452'

  tmux set-option -g status-justify centre
  tmux set-option -g status-style "bg=${comment_grey}"
  tmux set-option -g status-left ' #S '
  tmux set-option -g status-left-style "bg=${green},fg=${black}"

  tmux set-option -g status-right " CPU:#{cpu_percentage} #[bg=${special_grey}] %d/%m %R "
  tmux set-option -g status-right-style "bg=${menu_grey},fg=${white}"

  tmux set-window-option -g window-status-format ' #I:#W '
  tmux set-window-option -g window-status-style "bg=${menu_grey}"
  tmux set-window-option -g window-status-current-format ' #I:#W '
  tmux set-window-option -g window-status-current-style "bg=${green},fg=${black}"
  tmux set-window-option -g window-status-separator ''
}

main
```

###

