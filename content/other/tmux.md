
[[dev-notes]]

[[Tmux Cheatsheet]]

[[Syntactically correct .tmux.conf]]


---

```Bash
sudo apt install tmux

tmux kill-server
tmux kill-window -t <windowname>
```

```
tmux source-file ~/.tmux.conf
```
Press your tmux prefix key (default is `Ctrl+B`) followed by `:` to open the command prompt, then type `kill-window` and press Enter. Alternatively, you can use `Ctrl+B &` to kill the current window and confirm with `y` to really kill the window including all panes within it.


```
`tmux new -s myname` create new named session
`tmux a -t myname` to attach to names session
`ctrl b ,` to name window
```

vim/nvim esc lag issue fix:
	`set -s escape-time 0` in .tmux.conf


---
- open new window in same directory
add to tmux.conf
```
bind c new-window -c "#{pane_current_path}"
bind % split-window -h -c "#{pane_current_path}"
bind '"' split-window -v -c "#{pane_current_path}"
```
then
```
tmux source-file ~/.tmux.conf
```

```
press `prefix + I
```
---



# Save tmux sessions to persist restart

To save tmux sessions to persist a restart, you can use the tmux-resurrect plugin. This plugin saves all the details from your tmux environment so it can be completely restored after a system restart. To install tmux-resurrect, add the following line to your `.tmux.conf` file:

`set -g @plugin 'tmux-plugins/tmux-resurrect'`

After adding this line, press `prefix + I` within a tmux session to fetch and install the plugin. To save your tmux environment, press `prefix + Ctrl-s`. To restore the saved environment, you can use `prefix + Ctrl-r`.

For automatic saving and restoring of the tmux environment, you can also use the tmux-continuum plugin. This plugin saves the tmux environment every 15 minutes and can be installed similarly to tmux-resurrect.

To ensure vim sessions are restored, install Tim Pope’s vim-obsession plugin.

## Must press `prefix + I after installing

## .tmux.conf
```
bind c new-window -c "#{pane_current_path}"
bind '"' split-window -v -c "#{pane_current_path}"
bind % split-window -h -c "#{pane_current_path}"

set -s escape-time 0
set -g activity-action other
set -g assume-paste-time 1
set -g base-index 0
set -g bell-action any
set -g default-command ''
set -g default-shell /bin/bash
set -g default-size 80x24
set -g destroy-unattached off
set -g detach-on-destroy on
set -g display-panes-active-colour red
set -g display-panes-colour blue
set -g display-panes-time 1000
set -g display-time 750
set -g history-limit 2000
set -g key-table root
set -g lock-after-time 0
set -g lock-command "lock -np"
set -g message-command-style bg=black,fg=yellow
set -g message-style bg=yellow,fg=black
set -g mouse off
set -g prefix C-b
set -g prefix2 None
set -g renumber-windows off
set -g repeat-time 500
set -g set-titles off
set -g set-titles-string "#S:#I:#W - \"#T\" #{session_alerts}"
set -g silence-action other
set -g status on
set -g status-bg default
set -g status-fg default
set -g status-format[0] "#[align=left range=left #{status-left-style}]#[push-default]#{T;=/#{status-left-length}:status-left}#[pop-default]#[norange default]#[list=on align=#{status-justify}]#[list=left-marker]<#[list=right-marker]>#[list=on]#{W:#[range=window|#{window_index} #{window-status-style}#{?#{&&:#{window_last_flag},#{!=:#{window-status-last-style},default}}, #{window-status-last-style},}#{?#{&&:#{window_bell_flag},#{!=:#{window-status-bell-style},default}}, #{window-status-bell-style},#{?#{&&:#{||:#{window_activity_flag},#{window_silence_flag}},#{!=:#{window-status-activity-style},default}}, #{window-status-activity-style},}}]#[push-default]#{T:window-status-format}#[pop-default]#[norange default]#{?window_end_flag,,#{window-status-separator}},#[range=window|#{window_index} list=focus #{?#{!=:#{window-status-current-style},default},#{window-status-current-style},#{window-status-style}}#{?#{&&:#{window_last_flag},#{!=:#{window-status-last-style},default}}, #{window-status-last-style},}#{?#{&&:#{window_bell_flag},#{!=:#{window-status-bell-style},default}}, #{window-status-bell-style},#{?#{&&:#{||:#{window_activity_flag},#{window_silence_flag}},#{!=:#{window-status-activity-style},default}}, #{window-status-activity-style},}}]#[push-default]#{T:window-status-current-format}#[pop-default]#[norange list=on default]#{?window_end_flag,,#{window-status-separator}}}#[nolist align=right range=right #{status-right-style}]#[push-default]#{T;=/#{status-right-length}:status-right}#[pop-default]#[norange default]"
set -g status-format[1] "#[align=centre]#{P:#{?pane_active,#[reverse],}#{pane_index}[#{pane_width}x#{pane_height}]#[default] }"
set -g status-interval 15
set -g status-justify left
set -g status-keys emacs
set -g status-left "[#{session_name}] "
set -g status-left-length 10
set -g status-left-style default
set -g status-position bottom
set -g status-right "#{?window_bigger,[#{window_offset_x}#,#{window_offset_y}] ,}\"#{=21:pane_title}\" %H:%M %d-%b-%y"
set -g status-right-length 40
set -g status-right-style default
set -g status-style bg=green,fg=black
set -g update-environment[0] DISPLAY
set -g update-environment[1] KRB5CCNAME
set -g update-environment[2] SSH_ASKPASS
set -g update-environment[3] SSH_AUTH_SOCK
set -g update-environment[4] SSH_AGENT_PID
set -g update-environment[5] SSH_CONNECTION
set -g update-environment[6] WINDOWID
set -g update-environment[7] XAUTHORITY
set -g visual-activity off
set -g visual-bell off
set -g visual-silence off
set -g word-separators " "

# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'tmux-plugins/tmux-resurrect'
# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'github_username/plugin_name#branch'
# set -g @plugin 'git@github.com:user/plugin'
# set -g @plugin 'git@bitbucket.com:user/plugin'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'

```



## resize pane
In order to resize tmux panes, you first hit your tmux prefix (ctrl + b is the default one. Mine is ctrl + a.), and then the colon key :. This brings up a tmux command mode prompt at the bottom of your screen.
```
:resize-pane -L 20 # Resizes the current pane Left by 20 cells
:resize-pane -R 20 # Resizes the current pane Right by 20 cells
:resize-pane -D 20 # Resizes the current pane Down by 20 cells
:resize-pane -U 20 # Resizes the current pane Upward by 20 cells
```
