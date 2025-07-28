---
title: Complete Terminal Setup Guide for Ubuntu
draft: false
tags:
  - "#linux"
  - "#ubuntu"
  - "#setup"
aliases:
  - ubuntu basic setup
---
I've noticed that many friends who are starting to use Linux (particularly Ubuntu) struggle with terminal usage. Based on my experience and terminal setup, I'd like to share some tips that can significantly improve your command-line experience.

This guide covers four essential tools:

- **Zsh with Oh My Zsh** - Enhanced shell with auto-completion and syntax highlighting
- **Neovim** - Modern text editor setup
- **Tmux** - Terminal multiplexer for session management
- **Lazygit** - Visual Git interface

You can also find this setup on my GitHub: [Ubuntu Basic Setup](https://github.com/thejourneyofbabo/Ubuntu-Basic-Setup)

---
## 1. Zsh with Oh My Zsh Setup

### Quick Installation

```bash
# Install prerequisites
sudo apt install wget curl git fonts-powerline zsh

# Change default shell
chsh -s $(which zsh)

# Install Oh My Zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# Install essential plugins
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf && ~/.fzf/install
```

### Configuration

Edit `~/.zshrc`:

```bash
# Theme
ZSH_THEME="af-magic"

# Plugins
plugins=(git sudo colored-man-pages zsh-syntax-highlighting zsh-autosuggestions fzf)

# ROS2 auto complete
autoload -u bashcompinit
bashcompinit

# ROS2 aliases
alias cbr="colcon build --symlink-install --cmake-args -DCMAKE_BUILD_TYPE=Release"
alias cbrs="cbr --packages-skip"
alias cbp="colcon build --packages-select"
alias sor="source install/setup.zsh"
alias rlt="ros2 topic list"
alias rle="ros2 topic echo"
alias rli="ros2 topic info"
alias ril="ros2 interface list"
alias rill="ros2 interface list | grep"
alias rils="ros2 interface show"
alias rpe="ros2 pkg executables"

# System aliases
alias sr="source ~/.zshrc"
alias lz="lazygit"
```

Apply changes: `source ~/.zshrc`

---

## 2. Neovim Setup
[Download newest Neovim on Ubuntu](https://github.com/neovim/neovim/blob/master/BUILD.md)
### Installation

```bash
# Install dependencies
sudo apt install ninja-build gettext cmake unzip curl

# Build from source
git clone https://github.com/neovim/neovim
cd neovim && git checkout stable
make CMAKE_BUILD_TYPE=RelWithDebInfo
sudo make install
```

### Quick Theme Setup

**NvChad (Recommended):**

```bash
git clone https://github.com/NvChad/starter ~/.config/nvim && nvim
```

**Custom Configuration (Made by me. Focus on Rust):**

```bash
git clone https://github.com/thejourneyofbabo/clean-nvim.git ~/.config/nvim && nvim
```

---

## 3. Tmux Setup

### Installation

```bash
# Install packages
sudo apt install git xclip tmux

# Install TPM (Tmux Plugin Manager)
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

### Basic Configuration

Create `~/.tmux.conf`:

```bash
# Core Options
set -g mouse on
set -g default-terminal "tmux-256color"
set-option -sa terminal-overrides ",xterm*:Tc"

# Clipboard setup
set-option -g set-clipboard on
bind-key -T copy-mode-vi y send-keys -X copy-pipe-and-cancel "xclip -selection clipboard -in"

# Window and Pane Settings
set -g base-index 1
set -g pane-base-index 1
set-window-option -g pane-base-index 1
set-option -g renumber-windows on
set-window-option -g mode-keys vi

# Key Bindings
bind -n M-H previous-window
bind -n M-L next-window
bind-key -T copy-mode-vi v send-keys -X begin-selection
bind-key -T copy-mode-vi C-v send-keys -X rectangle-toggle
# bind-key -T copy-mode-vi y send-keys -X copy-selection-and-cancel
bind '"' split-window -v -c "#{pane_current_path}"
bind % split-window -h -c "#{pane_current_path}"

# Plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'christoomey/vim-tmux-navigator'
# set -g @plugin 'catppuccin/tmux'
set -g @plugin 'dreamsofcode-io/catppuccin-tmux'

set -g automatic-rename on
set -g automatic-rename-format '#{b:pane_current_path}'

# Initialize TPM (keep this line at the very end)
run '~/.tmux/plugins/tpm/tpm'
```

Install plugins: Start tmux, then press `Ctrl + b` + `I`

### Essential Commands

- **Sessions:** `tmux new -s name`, `tmux attach -t name`
- **Windows:** `Ctrl + b + c` (new), `Alt + H/L` (navigate)
- **Panes:** `Ctrl + b + "` (horizontal), `Ctrl + b + %` (vertical)

---

## 4. Lazygit - Visual Git Interface

### What is Lazygit?
[Lazygit github](https://github.com/jesseduffield/lazygit)
Lazygit provides a simple terminal UI for Git commands, making Git operations visual and intuitive without memorizing complex commands.

**Key Features:**

- Visual file staging and committing
- Easy branch switching and merging
- Interactive rebase and conflict resolution
- Built-in diff viewer

---

## Benefits of This Setup

### Productivity Gains

- **Visual feedback** with syntax highlighting and themes
- **Session persistence** with tmux for long-running tasks
- **Simplified Git workflow** with lazygit's visual interface

### Development Workflow

- **ROS2 aliases** speed up common tasks
- **Multiple terminal sessions** without losing context
- **Efficient editing** with modern Neovim configuration
- **Intuitive Git operations** reduce command-line errors

This setup transforms your terminal into a powerful development environment that significantly improves productivity and makes the command-line experience more enjoyable.