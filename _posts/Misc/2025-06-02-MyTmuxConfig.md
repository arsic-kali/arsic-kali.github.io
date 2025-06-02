---
title: Random Tips and Tricks
published: true
---

### [](#header-3)Below is my current Tmux Config:
Below are some features that it provides:
*   Displays IP address in the bottom left.
*   Allows for simple copy and paste by highlighting anything in your terminal and releasing.
*   Displays the date and time in the bottom right.
*   Adds color scheme to status bar, which can easily be tweaked to your liking.

#### [](#header-4)Remember to create/paste this into a .tmux.conf file:
```
# Enable mouse support
set -g mouse on
#set -g set-clipboard on
# Optional: Enable mouse wheel for scrolling in copy mode
setw -g mode-keys vi   # (optional but useful if you're used to vi-style navigation)

# Get the current IP and display it on the left of the status bar
set -g status-left-length 100
set -g status-left "#[fg=colour15]#(ip addr show | grep "inet[^6]" | awk '{print $2}')    "

# Setting right tmux status pane
set -g status-right-length 60
set -g status-right "#[fg=colour15,bold]%A, %B %d %Y — %l:%M %p"

# Activity Detected
setw -g monitor-activity on
set -g visual-activity off
set-option -gw window-status-activity-style fg=colour46,bg=black,blink

# Set overall status bar background to grey
set -g status-bg  black  # grey
set -g status-fg colour15 # text color

# Set active window title color
set -g window-status-current-style bg=black,fg=green

# Set inactive window title color
set -g window-status-style bg=black,fg=red

# Linux only
set -g mouse on
bind -n WheelUpPane if-shell -F -t = "#{mouse_any_flag}" "send-keys -M" "if -Ft= '#{pane_in_mode}' 'send-keys -M' 'select-pane -t=; copy-mode -e; send-keys -M'"
bind -n WheelDownPane select-pane -t= \; send-keys -M
bind -n C-WheelUpPane select-pane -t= \; copy-mode -e \; send-keys -M
bind -T copy-mode-vi    C-WheelUpPane   send-keys -X halfpage-up
bind -T copy-mode-vi    C-WheelDownPane send-keys -X halfpage-down
bind -T copy-mode-emacs C-WheelUpPane   send-keys -X halfpage-up
bind -T copy-mode-emacs C-WheelDownPane send-keys -X halfpage-down

# To copy, left click and drag to highlight text in yellow, 
# once you release left click yellow text will disappear and will automatically be available in clibboard
# Use vim keybindings in copy mode
setw -g mode-keys vi
# Update default binding of `Enter` to also use copy-pipe
unbind -T copy-mode-vi Enter
bind-key -T copy-mode-vi Enter send-keys -X copy-pipe-and-cancel "xclip -selection c"
bind-key -T copy-mode-vi MouseDragEnd1Pane send-keys -X copy-pipe-and-cancel "xclip -i -sel p -f | xclip -i -sel c"
```