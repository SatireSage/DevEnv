 SSH

## Setting Up ssh

Command: 
```bash
ssh username@vdt_address

```
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
CentOS7 -
```bash
sudo yum install tmux
```

Alma9 -
```bash
- sudo dnf install tmux
```

**Note:** If the above command does not work on your machine then you may use: `/usr/bin/sudo`

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

#### Common Commands:
Here's a list of common tmux commands:

1. `tmux new-session -s <session-name>`: Create a new session with a specified name.
2. `tmux attach -t <session-name>`: Attach to an existing session.
3. `tmux detach`: Detach from the current session.
4. `tmux list-sessions`: List all active sessions.
5. `tmux kill-session -t <session-name>`: Kill a specific session.

Within a tmux session, you can use the following commands, typically prefixed with a default key binding (`Ctrl+b`):

1. `Ctrl+b %`: Split the current pane vertically.
2. `Ctrl+b "`: Split the current pane horizontally.
3. `Ctrl+b o`: Move to the next pane.
4. `Ctrl+b ;`: Toggle between the current and previous pane.
5. `Ctrl+b x`: Close the current pane.
6. `Ctrl+b c`: Create a new window.
7. `Ctrl+b n`: Move to the next window.
8. `Ctrl+b p`: Move to the previous window.
9. `Ctrl+b w`: List all windows.
10. `Ctrl+b ,`: Rename the current window.
11. `Ctrl+b &`: Close the current window.

Remember, the default prefix key in tmux is `Ctrl+b`, but this can be changed in the tmux configuration file (`~/.tmux.conf`).

### Launch Tmux automatically:
Add the following to you cshell/bash shell scripts:

**For cshell:**
 - CentOS7: `~/.shellrc`
 - Alma9: `~/.tcshrc`
```csh
if ( $?prompt && ! $?TMUX && "$TERM" !~ "screen*" && "$TERM" !~ "tmux*" ) then
    if ( `which tmux` != "" ) then
        exec tmux
    endif
endif

```

**For bash:**
Alma9/CentOS7: `~/.bashrc`
```bash
if command -v tmux &> /dev/null && [ -n "$PS1" ] && [[ ! "$TERM" =~ screen ]] && [[ ! "$TERM" =~ tmux ]] && [ -z "$TMUX" ]; then
  exec tmux
fi
```

# Additional tools:
 - **zshell (zsh):** Advanced shell with scripting capabilities/Extensible with themes and plugins/Improved command-line experience with features like globbing and completion.
    * Oh My Zsh: Framework for managing Zsh configuration/Provides themes and plugins for customization/Eases setup and usage of Zsh for beginners and experts.
        * Zsh Autosuggestions: Suggests commands based on command history/Improves typing speed and reduces errors/Interactive and non-intrusive suggestions.
        * Zsh Autocomplete: Enhances command completion with smarter suggestions/Supports completion for commands, options, and arguments/Configurable and extensible with custom completions.
 - **neovim (nvim):** Improved version of Vim editor/Extensible with plugins and Lua scripting/Enhanced user interface and performance.
 - **fuzzy finder (fzf):** Quick file searching/Integration with command-line tools/Fuzzy matching for partial search queries.
 - **ripgrep (rg):** Better grep. Fast search tool for files/Uses regex patterns/Supports searching in large codebases.
 - **exa/eza:** Modern replacement for 'ls' command/Colorful output and extended file information/Supports Git status integration.
 - **zoxide (z):** Smart directory navigation/Tracks frequently visited directories/Quick jumping to directories with fuzzy matching.
 - **midnight commander (mc):** File manager with a text-based user interface/Dual-pane layout for easy file operations/Built-in file viewer and editor.
 - **bat:** Enhanced 'cat' command with syntax highlighting/Integrated Git support/Supports paging for large files.
 - **fd:**
 - **git-delta:**
 - **tlrc:**

# Cool stuff:
 - sl
 - pipes.sh
 - cmatrix
