# SSH

## Setting Up ssh

Command: ssh username@vdt_address

### Passwordless ssh

**Command:**
```bash
ssh-keygen -t ed25519

```
**Note:** If you are using a legacy system that doesn't support the Ed25519 algorithm, use:
```bash
ssh-keygen -t rsa -b 4096
```

Your public key has been saved in `C:\Users\[username]/.ssh/id_rsa.pub` if you didn’t change the file location.
Connect to the destination server using ssh and your password from PowerShell.Open the “authorized_keys” file with vi or nano:
`vi ~/.ssh/authorized_keys`
`nano ~/.ssh/authorized_keys`

Save your changes.
Now when you reconnect via ssh you will not be prompted for your credentials.

# Tmux

## Installing Tmux

**Command:**
```bash
CentOS7 - /usr/bin/sudo yum install tmux
```
```bash
Alma9 - sudo dnf install tmux
```

**Note:** If the above command does not work on your machine then you may use:
/usr/bin/sudo dnf install tmux

Before we launch tmux let's add some configurations

## Configuring Tmux

Create a tmux configuration file if it does not already exist at the following path: ~/.tmux.conf
Within this file we can configue our tmux.

### Basic Tmux configuration

**Reference the tmux.conf file:** [TmuxConfig](./README.md)

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

1. [Dracula](https://draculatheme.com/tmux)
2. [Catppuccin](https://github.com/catppuccin/tmux)

Follow the configuration steps within the respective links for using them.

### Tmux cheatsheet: [Cheatsheet](https://tmuxcheatsheet.com/)

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

