# SSH

## Setting Up ssh

Command: ssh username@vdt_address

### Passwordless ssh

Command: ssh-keygen -t ed25519
Note: If you are using a legacy system that doesn't support the Ed25519 algorithm, use:
ssh-keygen -t rsa -b 4096

Your public key has been saved in C:\Users\[username]/.ssh/id_rsa.pub if you didn’t change the file location.
Connect to the destination server using ssh and your password from PowerShell.Open the “authorized_keys” file with vi or nano:
vi ~/.ssh/authorized_keys
nano ~/.ssh/authorized_keys

Save your changes.
Now when you reconnect via ssh you will not be prompted for your credentials.

# Tmux

## Installing Tmux

Command:
CentOS7 - /usr/bin/sudo yum install tmux 
Alma9 - sudo dnf install tmux
Note: If the above command does not work on your machine then you may use:
/usr/bin/sudo dnf install tmux

Before we launch tmux let's add some configurations

## Configuring Tmux

Create a tmux configuration file if it does not already exist at the following path: ~/.tmux.conf
Within this file we can configue our tmux.

### Basic Tmux configuration

```markdown
# reload config file (change file location to your the tmux.conf you want to use)
bind r source-file ~/.tmux.conf 

# Enable mouse control (clickable windows, panes, resizable panes)
set -g mouse on

set -g base-index 1              # start indexing windows at 1 instead of 0
set -g renumber-windows on       # renumber all windows when any window is closed
set -g set-clipboard on          # use system set-clipboard

# split panes using v and h
bind h split-window -h
bind v split-window -v
unbind '"'
unbind %

# switch panes using Alt-arrow without prefix
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# Address vim mode switching delay (http://superuser.com/a/252717/65504)
set -s escape-time 0

set -g status-position top #Optional: sets the tmux status bar at the top

# increase history size 
set -g history-limit 1000000
# Increase tmux messages display duration from 750ms to 3s
set -g display-time 3000
# Refresh 'status-left' and 'status-right' more often, from every 15s to 5s
set -g status-interval 5
# Upgrade $TERM
set -g default-terminal "screen-256color"
# Focus events enabled for terminals that support them
set -g focus-events on
# Super useful when using "grouped sessions" and multi-monitor setup
setw -g aggressive-resize on

# Clock
setw -g clock-mode-colour colour0
setw -g clock-mode-style 12

# don't do anything when a 'bell' rings
set -g visual-activity off
set -g visual-bell off
set -g visual-silence off
setw -g monitor-activity off
set -g bell-action none

# copy mode
setw -g mode-style 'fg=colour1 bg=colour18 bold'

# pane borders
set -g pane-border-style 'fg=colour1'
set -g pane-active-border-style 'fg=colour3'

# statusbar
set -g status-position bottom
set -g status-justify left
set -g status-style 'fg=colour1'
set -g status-left ''
set -g status-right '%Y-%m-%d %H:%M '
set -g status-right-length 50
set -g status-left-length 10

setw -g window-status-current-style 'fg=colour0 bg=colour1 bold'
setw -g window-status-current-format ' #I #W #F '

setw -g window-status-style 'fg=colour1 dim'
setw -g window-status-format ' #I #[fg=colour7]#W #[fg=colour1]#F '

setw -g window-status-bell-style 'fg=colour2 bg=colour1 bold'

# messages
set -g message-style 'fg=colour2 bg=colour0 bold'

bind c new-window -c "#{pane_current_path}"

```

### Additional configurations: Plugins

#### Installing TPM
Stands for Tmux Plugin Manager. It allows you to create and install tmux plugins easily.
To install TPM, you need to:

1. Clone TPM: git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
2. Put this at the bottom of ~/.tmux.conf:
```markdown
# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'

# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'github_username/plugin_name#branch'
# set -g @plugin 'git@github.com:user/plugin'
# set -g @plugin 'git@bitbucket.com:user/plugin'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```
3. Reload TMUX environment so TPM is sourced. Use the keybind we set in our initial setup (prefix+r) or your own custom keybind.
```bash
# type this in terminal if tmux is already running
tmux source ~/.tmux.conf
```

That's it!

##### Installing plugins

1. Add new plugin to `~/.tmux.conf` with `set -g @plugin '...'`
2. Press `prefix` + <kbd>I</kbd> (capital i, as in **I**nstall) to fetch the plugin.

You're good to go! The plugin was cloned to `~/.tmux/plugins/` dir and sourced.

##### Uninstalling plugins

1. Remove (or comment out) plugin from the list.
2. Press `prefix` + <kbd>alt</kbd> + <kbd>u</kbd> (lowercase u as in **u**ninstall) to remove the plugin.

All the plugins are installed to `~/.tmux/plugins/` so alternatively you can
find plugin directory there and remove it.

##### Key bindings

`prefix` + <kbd>I</kbd>
- Installs new plugins from GitHub or any other git repository
- Refreshes TMUX environment

`prefix` + <kbd>U</kbd>
- updates plugin(s)

`prefix` + <kbd>alt</kbd> + <kbd>u</kbd>
- remove/uninstall plugins not on the plugin list

#### Additional Tmux: Themes

1. Dracula: https://draculatheme.com/tmux
2. Catppuccin: https://github.com/catppuccin/tmux

Follow the configuration steps within the respective links for using them.

### Tmux cheatsheet: https://tmuxcheatsheet.com/

<!---
Potentially add common commands
--->

### Launch Tmux automatically:
Add the following to you cshell/bash shell scripts:

CentOS7:  ~/.shellrc
Alma9: ~/.tcshrc or ~/.bashrc

<!---
Adding the command
--->

# Additional tools:
 - neovim (nvim)
 - fuzzy finder (fzf)
 - ripgrep (rg)
 - exa/eza
 - zoxide (z)
 - midnight commander (mc)
 - bat


