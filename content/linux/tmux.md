---
title: "git"
weight: 3
---
# tmux
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

## tmux Cheat Sheet
---
Tmux Cheat Sheet
Attach and detach
BY SETH KENLON
opensource.com CC BY-SA 4.0Mastodon fosstodon.org/@osdc

Attach and detach
$ tmux Start new tmux session
$ tmux attach Attach to tmux session running in the background
Ctrl+B d Detach from tmux session, leaving it running in the background
Ctrl+B & Exit and quit tmux
Ctrl+B ? List all key bindings (press Q to exit help screen)

Window Management
Ctrl+B C Create new window
Ctrl+B N Move to next window
Ctrl+B P Move to previous window
Ctrl+B L Move to last window
Ctrl+B 0-9 Move to window by index number

Ctrl+B ) Move to next session
Ctrl+B ( Move to previous session
Ctrl+B Ctrl+Z Suspend session


Split window into panes
Ctrl+B % Vertical split (panes side by side)
Ctrl+B " Horizontal split (one pane below the other)
Ctrl+B O Move to other pane
Ctrl+B ! Remove all panes but the current one from the window
Ctrl+B Q Display window index numbers
Ctrl+B Ctrl-Up/Down Resize current pane (due north/south)
Ctrl+B Ctrl-Left/Right Resize current pane (due west/east)

Multiplex
Ctrl+B : Access tmux command prompt
Ctrl+B :setw synchronize-panes on Synchronize panes (to send a command to many hosts)

opensource.com CC BY-SA 4.0

---
# tmux shortcuts & cheatsheet
start new:
    tmux
start new with session name:
    tmux new -s myname
attach:
    tmux a  #  (or at, or attach)
attach to named:
    tmux a -t myname
list sessions:
    tmux ls
<a name="killSessions"></a>kill session:
    tmux kill-session -t myname
<a name="killAllSessions"></a>Kill all the tmux sessions:
    tmux ls | grep : | cut -d. -f1 | awk '{print substr($1, 0, length($1)-1)}' | xargs kill
In tmux, hit the prefix `ctrl+b` (my modified prefix is ctrl+a) and then:
## List all shortcuts
to see all the shortcuts keys in tmux simply use the `bind-key ?` in my case that would be `CTRL-B ?`
## Sessions
    :new<CR>  new session
    s  list sessions
    $  name session
## <a name="WindowsTabs"></a>Windows (tabs)
    c  create window
    w  list windows
    n  next window
    p  previous window
    f  find window
    ,  name window
    &  kill window
## <a name="PanesSplits"></a>Panes (splits) 

    %  vertical split
    "  horizontal split
    o  swap panes
    q  show pane numbers
    x  kill pane
    +  break pane into window (e.g. to select text by mouse to copy)
    -  restore pane from window
    ⍽  space - toggle between layouts
    <prefix> q (Show pane numbers, when the numbers show up type the key to goto that pane)
    <prefix> { (Move the current pane left)
    <prefix> } (Move the current pane right)
    <prefix> z toggle pane zoom
## <a name="syncPanes"></a>Sync Panes 

You can do this by switching to the appropriate window, typing your Tmux prefix (commonly Ctrl-B or Ctrl-A) and then a colon to bring up a Tmux command line, and typing:

```
:setw synchronize-panes
```

You can optionally add on or off to specify which state you want; otherwise the option is simply toggled. This option is specific to one window, so it won’t change the way your other sessions or windows operate. When you’re done, toggle it off again by repeating the command. [tip source](http://blog.sanctum.geek.nz/sync-tmux-panes/)
## Resizing Panes

You can also resize panes if you don’t like the layout defaults. I personally rarely need to do this, though it’s handy to know how. Here is the basic syntax to resize panes:

    PREFIX : resize-pane -D (Resizes the current pane down)
    PREFIX : resize-pane -U (Resizes the current pane upward)
    PREFIX : resize-pane -L (Resizes the current pane left)
    PREFIX : resize-pane -R (Resizes the current pane right)
    PREFIX : resize-pane -D 20 (Resizes the current pane down by 20 cells)
    PREFIX : resize-pane -U 20 (Resizes the current pane upward by 20 cells)
    PREFIX : resize-pane -L 20 (Resizes the current pane left by 20 cells)
    PREFIX : resize-pane -R 20 (Resizes the current pane right by 20 cells)
    PREFIX : resize-pane -t 2 -L 20 (Resizes the pane with the id of 2 left by 20 cells)
## Copy mode:

Pressing PREFIX [ places us in Copy mode. We can then use our movement keys to move our cursor around the screen. By default, the arrow keys work. we set our configuration file to use Vim keys for moving between windows and resizing panes so we wouldn’t have to take our hands off the home row. tmux has a vi mode for working with the buffer as well. To enable it, add this line to .tmux.conf:

    setw -g mode-keys vi

With this option set, we can use h, j, k, and l to move around our buffer.

To get out of Copy mode, we just press the ENTER key. Moving around one character at a time isn’t very efficient. Since we enabled vi mode, we can also use some other visible shortcuts to move around the buffer.

For example, we can use "w" to jump to the next word and "b" to jump back one word. And we can use "f", followed by any character, to jump to that character on the same line, and "F" to jump backwards on the line.

       Function                vi             emacs
       Back to indentation     ^              M-m
       Clear selection         Escape         C-g
       Copy selection          Enter          M-w
       Cursor down             j              Down
       Cursor left             h              Left
       Cursor right            l              Right
       Cursor to bottom line   L
       Cursor to middle line   M              M-r
       Cursor to top line      H              M-R
       Cursor up               k              Up
       Delete entire line      d              C-u
       Delete to end of line   D              C-k
       End of line             $              C-e
       Goto line               :              g
       Half page down          C-d            M-Down
       Half page up            C-u            M-Up
       Next page               C-f            Page down
       Next word               w              M-f
       Paste buffer            p              C-y
       Previous page           C-b            Page up
       Previous word           b              M-b
       Quit mode               q              Escape
       Scroll down             C-Down or J    C-Down
       Scroll up               C-Up or K      C-Up
       Search again            n              n
       Search backward         ?              C-r
       Search forward          /              C-s
       Start of line           0              C-a
       Start selection         Space          C-Space
       Transpose chars                        C-t

## Misc

    d  detach
    t  big clock
    ?  list shortcuts
    :  prompt

## Configurations Options:

    # Mouse support - set to on if you want to use the mouse
    * setw -g mode-mouse off
    * set -g mouse-select-pane off
    * set -g mouse-resize-pane off
    * set -g mouse-select-window off

    # Set the default terminal mode to 256color mode
    set -g default-terminal "screen-256color"

    # enable activity alerts
    setw -g monitor-activity on
    set -g visual-activity on

    # Center the window list
    set -g status-justify centre

    # Maximize and restore a pane
    unbind Up bind Up new-window -d -n tmp \; swap-pane -s tmp.1 \; select-window -t tmp
    unbind Down
    bind Down last-window \; swap-pane -s tmp.1 \; kill-window -t tmp

## Resources:

* [tmux: Productive Mouse-Free Development](http://pragprog.com/book/bhtmux/tmux)
* [How to reorder windows](http://superuser.com/questions/343572/tmux-how-do-i-reorder-my-windows)

* Twitter: [@MohammedAlaa](http://twitter.com/MohammedAlaa)
