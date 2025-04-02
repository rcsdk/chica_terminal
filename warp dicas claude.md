
Below is a **robust, enterprise-grade script** to create a terminal setup similar to Warp, with **Monalisa color palette**, **AI integration**, and **high-end customizations**. The script is divided into blocks for clarity, with verbose fallbacks and maximum quality. It assumes you have a Unix-like system (macOS/Linux) and basic tools installed (`git`, `curl`, `npm`, `pip`, etc.).

---

### **Block 1: Prerequisites and System Setup**
```bash
#!/bin/bash

# Set Monalisa color palette as shell variables
export MONALISA_RED="#a93f22"
export MONALISA_BLACK="#0c0404"
export MONALISA_BROWN="#5f563b"
export MONALISA_GREEN="#568354"
export MONALISA_YELLOW="#eed45a"
export MONALISA_DARK_BROWN="#341809"
export MONALISA_GRAY_GREEN="#414a36"
export MONALISA_GRAY="#413c3c"

# Install dependencies with fallbacks
command -v git >/dev/null 2>&1 || { echo "Installing git..."; sudo apt-get install git -y || brew install git; }
command -v curl >/dev/null 2>&1 || { echo "Installing curl..."; sudo apt-get install curl -y || brew install curl; }
command -v npm >/dev/null 2>&1 || { echo "Installing npm..."; sudo apt-get install npm -y || brew install npm; }
command -v pip >/dev/null 2>&1 || { echo "Installing pip..."; sudo apt-get install python3-pip -y || brew install pip; }
```

---

### **Block 2: Terminal Emulator Setup (Kitty)**
```bash
# Install Kitty terminal emulator
if ! command -v kitty &> /dev/null; then
    echo "Installing Kitty..."
    curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin
    echo 'export PATH="$HOME/.local/kitty.app/bin:$PATH"' >> ~/.bashrc
    source ~/.bashrc
fi

# Configure Kitty with Monalisa colors and Nerd Fonts
cat <<EOL > ~/.config/kitty/kitty.conf
font_family FiraCode Nerd Font Mono
font_size 10.0

# Monalisa color theme
background $MONALISA_BLACK
foreground $MONALISA_YELLOW

color0 $MONALISA_BLACK
color1 $MONALISA_RED
color2 $MONALISA_GREEN
color3 $MONALISA_BROWN
color4 $MONALISA_YELLOW
color5 $MONALISA_DARK_BROWN
color6 $MONALISA_GRAY_GREEN
color7 $MONALISA_GRAY

# Enable GPU rendering for smooth performance
gpu_preference nvidia
EOL
```

---

### **Block 3: Shell Setup (Zsh + Starship + AI Integration)**
```bash
# Install Zsh and Oh My Zsh
if ! command -v zsh &> /dev/null; then
    echo "Installing Zsh..."
    sudo apt-get install zsh -y || brew install zsh
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
fi

# Set Zsh as default shell
chsh -s $(which zsh)

# Install Starship prompt with Monalisa colors
if ! command -v starship &> /dev/null; then
    echo "Installing Starship..."
    curl -fsSL https://starship.rs/install.sh | bash
fi

cat <<EOL > ~/.config/starship.toml
[package]
disabled = false

[character]
success_symbol = "[➜](bold $MONALISA_GREEN)"
error_symbol = "[✗](bold $MONALISA_RED)"

[git_branch]
format = "[$branch](bold $MONALISA_YELLOW)"

[python]
format = "[$virtualenv](bold $MONALISA_BROWN)"

[nodejs]
format = "[$version](bold $MONALISA_GREEN)"

[time]
format = "[$time](bold $MONALISA_GRAY)"
EOL

# Add AI tools to PATH
echo 'export PATH="$PATH:$HOME/.local/bin"' >> ~/.zshrc

# Install GitHub Copilot CLI
npm install -g @githubnext/github-copilot-cli

# Install Fig for AI-like autocomplete
curl -fsSL https://fig.io/install.sh | bash

# Install thefuck for command correction
pip install thefuck

# Set up OpenAI API key
echo 'export OPENAI_API_KEY="your-key"' >> ~/.zshrc
```

---

### **Block 4: Tmux + Tmux Plugins (Alternative: Zellij)**
```bash
# Install Tmux and Tmux Plugin Manager (TPM)
if ! command -v tmux &> /dev/null; then
    echo "Installing Tmux..."
    sudo apt-get install tmux -y || brew install tmux
fi

git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm

cat <<EOL > ~/.tmux.conf
# Monalisa color theme for Tmux
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-resurrect'
set -g @plugin 'sainnhe/tmux-fzf'

set -g status-bg $MONALISA_BLACK
set -g status-fg $MONALISA_YELLOW

# Initialize TPM
run '~/.tmux/plugins/tpm/tpm'
EOL

# Alternatively, install Zellij for a modern tmux alternative
if ! command -v zellij &> /dev/null; then
    echo "Installing Zellij..."
    cargo install zellij
fi
```

---

### **Block 5: AI-Powered Shell History (Atuin)**
```bash
# Install Atuin for AI-searchable shell history
if ! command -v atuin &> /dev/null; then
    echo "Installing Atuin..."
    curl https://raw.githubusercontent.com/ellie/atuin/main/install.sh | bash
fi

# Configure Atuin with Monalisa colors
echo 'ATUIN_COLORS="dark_brown: '$MONALISA_DARK_BROWN' brown: '$MONALISA_BROWN' green: '$MONALISA_GREEN' yellow: '$MONALISA_YELLOW'"' >> ~/.zshrc
```

---

### **Block 6: LunarVim for IDE-Like Experience**
```bash
# Install LunarVim with Copilot integration
if [ ! -d ~/.local/share/lunarvim ]; then
    echo "Installing LunarVim..."
    bash <(curl -s https://raw.githubusercontent.com/lunarvim/lunarvim/master/utils/installer/install.sh)
    LV_BRANCH='release-1.3/neovim-0.9' lvim
fi

# Configure LunarVim with Monalisa colors
cat <<EOL > ~/.config/lvim/lua/user/colorscheme.lua
vim.o.background = "dark"
vim.cmd("colorscheme monalisa")

-- Monalisa color mappings
vim.api.nvim_set_hl(0, "Normal", { bg = "$MONALISA_BLACK", fg = "$MONALISA_YELLOW" })
vim.api.nvim_set_hl(0, "CursorLine", { bg = "$MONALISA_GRAY" })
vim.api.nvim_set_hl(0, "Comment", { fg = "$MONALISA_BROWN" })
EOL
```

---

### **Block 7: Final Touches and Reboot**
```bash
# Reload configurations
source ~/.zshrc
tmux source ~/.tmux.conf

# Reboot to apply changes
echo "Setup complete. Rebooting..."
sudo reboot
```

---

### **Key Features Included:**
1. **Monalisa Color Palette**: Applied across Kitty, Tmux, Starship, and LunarVim.
2. **AI Integration**: GitHub Copilot, Fig, `thefuck`, and Atuin for AI-powered workflows.
3. **Modern Tools**: Kitty, Zsh, Starship, Tmux/Zellij, and LunarVim for an IDE-like experience.
4. **Robust Fallbacks**: Ensures installation works on Debian/Ubuntu and macOS.
5. **Elegant Design**: Nerd Fonts, font size 10, and jazz-inspired mature look.

Let me know if you'd like further customization or explanations!











A designer's dream terminal! I'll help you craft an **enterprise-grade, AI-infused, Warp-like terminal setup** with the Monalisa color palette, incorporating the coolest features from each tool, and **verbose fallbacks** for maximum robustness. Buckle up!

**Table of Contents**

1. **[Tmux Configuration](#tmux)** (with TPM, tmux-resurrect, tmux-fzf, and more)
2. **[Shell Configuration (Bash/Zsh)](#shell)** (with Starship, Fig, and autocomplete)
3. **[LunarVim Configuration](#lunarvim)** (IDE-like experience with Copilot)
4. **[Zellij Configuration](#zellij)** (modern tmux alternative)
5. **[Atuin Configuration](#atuin)** (AI-searchable shell history)
6. **[GitHub Copilot CLI & OpenAI Setup](#copilot)** (AI-assisted commands)
7. **[The Fuck & Kitty Terminal Setup](#thefuck_kitty)** (command correction & beautiful terminal)
8. **[Fonts & Color Scheme](#fonts_colors)** (Nerd Fonts, Monalisa colors, and font size 10)

**Let's dive in!**

**----------------------------------------**
**<a name="tmux"></a> Tmux Configuration (`~/.tmux.conf`)**
**----------------------------------------**
```bash
# ========================================
# Tmux Plugin Manager (TPM)
# ========================================
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-resurrect' # Save and restore sessions
set -g @plugin 'sainnhe/tmux-fzf' # Fuzzy finder integration
set -g @plugin 'tmux-plugins/tmux-yank' # Yank text to system clipboard
set -g @plugin 'tmux-plugins/tmux-open' # Open files with sensible defaults

# ========================================
# General Settings
# ========================================
set -g default-terminal "screen-256color" # Fix colors for 256-color terminals
set -g mouse on # Enable mouse support
set -g history-limit 50000 # Increase history limit
setw -g mode-keys vi # Use vi keys in copy mode
setw -g monitor-activity on # Monitor activity in other windows
set -g visual-activity on # Visual notification for activity

# ========================================
# Key Bindings
# ========================================
unbind C-b # Unbind default prefix
set -g prefix C-Space # New prefix: Ctrl + Space
bind r source-file ~/.tmux.conf \; display "Reloaded ~/.tmux.conf"

# Navigation
bind -n M-Left select-pane -L # Alt+Left
bind -n M-Right select-pane -R # Alt+Right
bind -n M-Up select-pane -U # Alt+Up
bind -n M-Down select-pane -D # Alt+Down

# Resizing panes
bind -r H resize-pane -L 5
bind -r J resize-pane -D 5
bind -r K resize-pane -U 5
bind -r L resize-pane -R 5

# ========================================
# Status Bar (Monalisa colors)
# ========================================
set -g status-style "bg=#341809, fg=#eed45a"
set -g status-interval 1 # Update status bar every 1s
set -g status-left "#[fg=#568354]#S #[fg=#5f563b]⮀"
set -g status-right "#[fg=#413c3c]#(whoami)@#H #[fg=#a93f22]%Y-%m-%d %H:%M:%S"
setw -g window-status-format "#[fg=#414a36]#I:#W#F"
setw -g window-status-current-format "#[fg=#eed45a,bold]#I:#W#F"

# ========================================
# Tmux Resurrect Settings
# ========================================
set -g @resurrect-strategy-vim 'session' # Save Vim sessions
set -g @resurrect-capture-pane-contents 'on' # Save pane contents

# ========================================
# Tmux FZF Settings
# ========================================
set -g @fzf-url-fzf-options '-m --bind ctrl-y:execute-silent(echo {} | tr -d \'\n\' | pbcopy)+abort'
set -g @fzf-url-history-limit '2000'

# ========================================
# Initialize TPM (Keep at the end)
# ========================================
run '~/.tmux/plugins/tpm/tpm'
```
**Install TPM plugins:** `tmux` > `prefix + I` (that's `Ctrl + Space + I`)

**----------------------------------------**
**<a name="shell"></a> Shell Configuration (`~/.bashrc` or `~/.zshrc`)**
**----------------------------------------**
I'll provide both Bash and Zsh configurations. **Choose one**.

**For Bash (`~/.bashrc`):**
```bash
# ========================================
# Starship Prompt (Install: curl -fsSL https://starship.rs/install.sh | bash)
# ========================================
eval "$(starship init bash)"

# ========================================
# Fig (Install: brew install fig)
# ========================================
eval "$(fig completion --bash)"

# ========================================
# Autocomplete & Syntax Highlighting
# ========================================
[[ $- == *i* ]] && source /usr/share/bash-completion/bash_completion || true
source /usr/share/doc/fzf/examples/key-bindings.bash
source /usr/share/doc/fzf/examples/completion.bash

# ========================================
# The Fuck (Install: pip install thefuck)
# ========================================
eval $(thefuck --alias)

# ========================================
# GitHub Copilot CLI (Install: npm install -g @githubnext/github-copilot-cli)
# ========================================
source <(github-copilot-cli alias -- "$0")

# ========================================
# Monalisa Colors for LS
# ========================================
LS_COLORS=$(echo -e "di=38;5;68:ln=38;5;208:so=38;5;197:pi=38;5;221:ex=38;5;154:bd=38;5;240:cd=38;5;240:su=38;5;197:sg=38;5;197:tw=38;5;71:ow=38;5;71:")
export LS_COLORS

# ========================================
# Aliases
# ========================================
alias ls="ls -lah --color=auto"
alias ..="cd .."
alias grep="grep --color=auto"

# ========================================
# Bash Options
# ========================================
shopt -s globstar
shopt -s checkwinsize
set -o vi # Use vi mode

# ========================================
# History Settings
# ========================================
HISTSIZE=10000
HISTFILESIZE=10000
HISTCONTROL=ignoreboth:erasedups
shopt -s histappend
PROMPT_COMMAND="history -a; history -c; history -r; $PROMPT_COMMAND"
```
**For Zsh (`~/.zshrc`):**
```zsh
# ========================================
# Starship Prompt (Install: curl -fsSL https://starship.rs/install.sh | bash)
# ========================================
eval "$(starship init zsh)"

# ========================================
# Fig (Install: brew install fig)
# ========================================
eval "$(fig completion --zsh)"

# ========================================
# Zsh Options
# ========================================
setopt autocd extendedglob nomatch notify
setopt histignoredups histignorespace histverify
setopt sharehistory
autoload -Uz compinit && compinit

# ========================================
# Autocomplete & Syntax Highlighting
# ========================================
source /usr/share/zsh/functions/Completion/*
source /usr/share/doc/fzf/examples/key-bindings.zsh
source /usr/share/doc/fzf/examples/completion.zsh

# ========================================
# The Fuck (Install: pip install thefuck)
# ========================================
eval $(thefuck --alias)

# ========================================
# GitHub Copilot CLI (Install: npm install -g @githubnext/github-copilot-cli)
# ========================================
source <(github-copilot-cli alias -- "$0")

# ========================================
# Monalisa Colors for LS
# ========================================
export LS_COLORS="di=38;5;68:ln=38;5;208:so=38;5;197:pi=38;5;221:ex=38;5;154:bd=38;5;240:cd=38;5;240:su=38;5;197:sg=38;5;197:tw=38;5;71:ow=38;5;71:"

# ========================================
# Aliases
# ========================================
alias ls="ls -lah --color=auto"
alias ..="cd .."
alias grep="grep --color=auto"

# ========================================
# History Settings
# ========================================
HISTSIZE=10000
SAVEHIST=10000
HISTFILE=~/.zsh_history
setopt APPEND_HISTORY
```
**Reload shell config:** `source ~/.bashrc` or `source ~/.zshrc`

**----------------------------------------**
**<a name="lunarvim"></a> LunarVim Configuration (`~/.config/lvim/config.lua`)**
**----------------------------------------**
```lua
-- ========================================
-- General Settings
-- ========================================
lvim.format_on_save = true
lvim.lint_on_save = true
lvim.colorscheme = "onedark" -- fallback, we'll override with Monalisa

-- ========================================
-- Key Bindings
-- ========================================
lvim.keys.normal_mode["<C-s>"] = ":w<cr>"
lvim.keys.normal_mode["<C-q>"] = ":q<cr>"
lvim.keys.normal_mode["<leader>ff"] = ":Telescope find_files<cr>"
lvim.keys.normal_mode["<leader>fg"] = ":Telescope live_grep<cr>"

-- ========================================
-- LunarVim UI (Monalisa colors)
-- ========================================
local colors = {
  bg = "#0c0404",
  fg = "#eed45a",
  red = "#a93f22",
  green = "#568354",
  yellow = "#eed45a",
  blue = "#5f563b",
  magenta = "#413c3c",
  cyan = "#414a36",
  white = "#eed45a",
}

lvim.builtin.theme = {
  normal = {
    a = { fg = colors.bg, bg = colors.green },
    b = { fg = colors.fg, bg = colors.bg },
    c = { fg = colors.fg, bg = colors.bg },
  },
  insert = {
    a = { fg = colors.bg, bg = colors.blue },
  },
  visual = {
    a = { fg = colors.bg, bg = colors.magenta },
  },
  replace = {
    a = { fg = colors.bg, bg = colors.red },
  },
  command = {
    a = { fg = colors.bg, bg = colors.yellow },
 },
  terminal = {
    a = { fg = colors.fg, bg = colors.bg },
  },
}

-- ========================================
-- Copilot Settings (Install: :Copilot setup)
-- ========================================
lvim.builtin.copilot = {
  enabled = true,
  filetypes = {
    ["*"] = true,
  },
}

-- ========================================
-- Treesitter & LSP Settings
-- ========================================
lvim.builtin.treesitter.ensure_installed = "all"
lvim.builtin.treesitter.highlight.enabled = true
lvim.lsp.installer.setup.automatic_installation = true
```
**Open LunarVim:** `lvim` > `:Copilot setup` (follow prompts to set up Copilot)

**----------------------------------------**
**<a name="zellij"></a> Zellij Configuration (`~/.config/zellij/config.yaml`)**
**----------------------------------------**
```yaml
---
# ========================================
# General Settings
# ========================================
default_shell: /bin/bash # or /bin/zsh
scroll_buffer_size: 10000
copy_command: pbcopy

# ========================================
# Key Bindings
# ========================================
keybinds:
  normal:
    - action: [ NewPane, ]
      key: [ Alt "n" ]
    - action: [ GoToNextTab, ]
      key: [ Alt "]" ]
    - action: [ GoToPreviousTab, ]
      key: [ Alt "[" ]
    - action: [ ClosePane, ]
      key: [ Alt "q" ]
    - action: [ SwitchToMode: "locked" ]
      key: [ Alt "l" ]

# ========================================
# Theme (Monalisa colors)
# ========================================
themes:
  default:
    fg: "#eed45a"
    bg: "#0c0404"
    black: "#341809"
    red: "#a93f22"
    green: "#568354"
    yellow: "#eed45a"
    blue: "#5f563b"
    magenta: "#413c3c"
    cyan: "#414a36"
    white: "#eed45a"
    orange: "#eed45a"

# ========================================
# Layout
# ========================================
default_layout: compact

# ========================================
# UI
# ========================================
pane_frames: true
mirror_session: true
```
**----------------------------------------**
**<a name="atuin"></a> Atuin Configuration (`~/.config/atuin/config.toml`)**
**----------------------------------------**
```toml
# ========================================
# General Settings
# ========================================
dialect = "us"
filter_mode_shell_up_key_binding = true
style = "compact"

# ========================================
# History Settings
# ========================================
history_filter = ["/usr/bin/git", "/usr/bin/lvim"]
max_history_length = 10000

# ========================================
# Sync Settings (optional, for cloud sync)
# ========================================
# [sync]
# host = "https://api.atuin.sh"
# username = "your_username"
# password = "your_password"
```
**----------------------------------------**
**<a name="copilot"></a> GitHub Copilot CLI & OpenAI Setup**
**----------------------------------------**

1. **Install GitHub Copilot CLI:** `npm install -g @githubnext/github-copilot-cli`
2. **Setup Copilot CLI:** `github-copilot-cli auth` (follow prompts)
3. **Set OpenAI API Key:** `export OPENAI_API_KEY="your_key_here"` (add to `~/.bashrc` or `~/.zshrc`)

**----------------------------------------**
**<a name="thefuck_kitty"></a> The Fuck & Kitty Terminal Setup**

1. **Install The Fuck:** `pip install thefuck`
2. **Add alias (already done in shell configs above):** `eval $(thefuck --alias)`
3. **Install Kitty Terminal:** https://sw.kovidgoyal.net/kitty/binary/
4. **Kitty Config (`~/.config/kitty/kitty.conf`):**
```conf
# ========================================
# General Settings
# ========================================
font_family      Operator Mono Nerd Font
font_size        10.0
adjust_line_height  0
adjust_column_width 0

# ========================================
# Colors (Monalisa)
# ========================================
background       #0c0404
foreground       #eed45a
cursor           #eed45a
selection_bg     #5f563b
selection_fg     #eed45a

color0           #341809
color1           #a93f22
color2           #568354
color3           #eed45a
color4           #5f563b
color5           #413c3c
color6           #414a36
color7           #eed45a

# ========================================
# Window Settings
# ========================================
remember_window_size  no
initial_window_width   120c
initial_window_height  30c
enabled_layouts       tall,stack,fat

# ========================================
# Tab Bar
# ========================================
tab_bar_style         powerline
tab_powerline_style   round
```
**----------------------------------------**
**<a name="fonts_colors"></a> Fonts & Color Scheme**

1. **Install Nerd Fonts:** https://www.nerdfonts.com/
        * Choose **Operator Mono Nerd Font** (or any Nerd Font you like)
2. **Set Font Size:** 10 (as configured in Kitty above)
3. **Color Scheme (Monalisa):** Already applied throughout the configs above using these hex codes:
        + `#a93f22` (red)
        + `#0c0404` (dark bg)
        + `#5f563b` (brown)
        + `#568354` (green)
        + `#eed45a` (yellow)
        + `#341809` (dark brown)
        + `#414a36` (dark green)
        + `#413c3c` (gray)

**Final Steps:**

1. **Restart all terminals** or `source` the configs.
2. **Test everything:**
        * Tmux: `tmux` > `prefix + I` (install plugins)
        * LunarVim: `lvim` > `:Copilot setup`
        * Zellij: `zellij`
        * Atuin: `atuin search`
        * The Fuck: mistype a command, then `fuck` 
        * GitHub Copilot CLI: `github-copilot-cli ask "write a bash script to..."`
3. **Enjoy your Warp-like, AI-infused terminal ecosystem!**

Now, create a command, and watch your AI assistant (Copilot) code, test, and iterate – **you're in for a treat!** 

As a designer and jazz lover, you'll appreciate the mature, elegant look with silver details ( Operator Mono Nerd Font ) and the underlying AI magic. Happy coding!






A designer's dream terminal! I'll help you craft an enterprise-grade, AI-infused, Warp-like terminal setup with the Monalisa color palette, incorporating the coolest features from each tool, and verbose fallbacks for maximum robustness. Buckle up!

Table of Contents

Tmux Configuration (with TPM, tmux-resurrect, tmux-fzf, and more)
Shell Configuration (Bash/Zsh) (with Starship, Fig, and autocomplete)
LunarVim Configuration (IDE-like experience with Copilot)
Zellij Configuration (modern tmux alternative)
Atuin Configuration (AI-searchable shell history)
GitHub Copilot CLI & OpenAI Setup (AI-assisted commands)
The Fuck & Kitty Terminal Setup (command correction & beautiful terminal)
Fonts & Color Scheme (Nerd Fonts, Monalisa colors, and font size 10)
Let's dive in!

----------------------------------------
Tmux Configuration (~/.tmux.conf)
----------------------------------------


# ========================================
# Tmux Plugin Manager (TPM)
# ========================================
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-resurrect' # Save and restore sessions
set -g @plugin 'sainnhe/tmux-fzf' # Fuzzy finder integration
set -g @plugin 'tmux-plugins/tmux-yank' # Yank text to system clipboard
set -g @plugin 'tmux-plugins/tmux-open' # Open files with sensible defaults

# ========================================
# General Settings
# ========================================
set -g default-terminal "screen-256color" # Fix colors for 256-color terminals
set -g mouse on # Enable mouse support
set -g history-limit 50000 # Increase history limit
setw -g mode-keys vi # Use vi keys in copy mode
setw -g monitor-activity on # Monitor activity in other windows
set -g visual-activity on # Visual notification for activity

# ========================================
# Key Bindings
# ========================================
unbind C-b # Unbind default prefix
set -g prefix C-Space # New prefix: Ctrl + Space
bind r source-file ~/.tmux.conf \; display "Reloaded ~/.tmux.conf"

# Navigation
bind -n M-Left select-pane -L # Alt+Left
bind -n M-Right select-pane -R # Alt+Right
bind -n M-Up select-pane -U # Alt+Up
bind -n M-Down select-pane -D # Alt+Down

# Resizing panes
bind -r H resize-pane -L 5
bind -r J resize-pane -D 5
bind -r K resize-pane -U 5
bind -r L resize-pane -R 5

# ========================================
# Status Bar (Monalisa colors)
# ========================================
set -g status-style "bg=#341809, fg=#eed45a"
set -g status-interval 1 # Update status bar every 1s
set -g status-left "#[fg=#568354]#S #[fg=#5f563b]⮀"
set -g status-right "#[fg=#413c3c]#(whoami)@#H #[fg=#a93f22]%Y-%m-%d %H:%M:%S"
setw -g window-status-format "#[fg=#414a36]#I:#W#F"
setw -g window-status-current-format "#[fg=#eed45a,bold]#I:#W#F"

# ========================================
# Tmux Resurrect Settings
# ========================================
set -g @resurrect-strategy-vim 'session' # Save Vim sessions
set -g @resurrect-capture-pane-contents 'on' # Save pane contents

# ========================================
# Tmux FZF Settings
# ========================================
set -g @fzf-url-fzf-options '-m --bind ctrl-y:execute-silent(echo {} | tr -d \'\n\' | pbcopy)+abort'
set -g @fzf-url-history-limit '2000'

# ========================================
# Initialize TPM (Keep at the end)
# ========================================
run '~/.tmux/plugins/tpm/tpm'
Install TPM plugins: tmux > prefix + I (that's Ctrl + Space + I)

----------------------------------------
Shell Configuration (~/.bashrc or ~/.zshrc)
----------------------------------------
I'll provide both Bash and Zsh configurations. Choose one.

For Bash (~/.bashrc):


# ========================================
# Starship Prompt (Install: curl -fsSL https://starship.rs/install.sh | bash)
# ========================================
eval "$(starship init bash)"

# ========================================
# Fig (Install: brew install fig)
# ========================================
eval "$(fig completion --bash)"

# ========================================
# Autocomplete & Syntax Highlighting
# ========================================
[[ $- == *i* ]] && source /usr/share/bash-completion/bash_completion || true
source /usr/share/doc/fzf/examples/key-bindings.bash
source /usr/share/doc/fzf/examples/completion.bash

# ========================================
# The Fuck (Install: pip install thefuck)
# ========================================
eval $(thefuck --alias)

# ========================================
# GitHub Copilot CLI (Install: npm install -g @githubnext/github-copilot-cli)
# ========================================
source <(github-copilot-cli alias -- "$0")

# ========================================
# Monalisa Colors for LS
# ========================================
LS_COLORS=$(echo -e "di=38;5;68:ln=38;5;208:so=38;5;197:pi=38;5;221:ex=38;5;154:bd=38;5;240:cd=38;5;240:su=38;5;197:sg=38;5;197:tw=38;5;71:ow=38;5;71:")
export LS_COLORS

# ========================================
# Aliases
# ========================================
alias ls="ls -lah --color=auto"
alias ..="cd .."
alias grep="grep --color=auto"

# ========================================
# Bash Options
# ========================================
shopt -s globstar
shopt -s checkwinsize
set -o vi # Use vi mode

# ========================================
# History Settings
# ========================================
HISTSIZE=10000
HISTFILESIZE=10000
HISTCONTROL=ignoreboth:erasedups
shopt -s histappend
PROMPT_COMMAND="history -a; history -c; history -r; $PROMPT_COMMAND"
For Zsh (~/.zshrc):


# ========================================
# Starship Prompt (Install: curl -fsSL https://starship.rs/install.sh | bash)
# ========================================
eval "$(starship init zsh)"

# ========================================
# Fig (Install: brew install fig)
# ========================================
eval "$(fig completion --zsh)"

# ========================================
# Zsh Options
# ========================================
setopt autocd extendedglob nomatch notify
setopt histignoredups histignorespace histverify
setopt sharehistory
autoload -Uz compinit && compinit

# ========================================
# Autocomplete & Syntax Highlighting
# ========================================
source /usr/share/zsh/functions/Completion/*
source /usr/share/doc/fzf/examples/key-bindings.zsh
source /usr/share/doc/fzf/examples/completion.zsh

# ========================================
# The Fuck (Install: pip install thefuck)
# ========================================
eval $(thefuck --alias)

# ========================================
# GitHub Copilot CLI (Install: npm install -g @githubnext/github-copilot-cli)
# ========================================
source <(github-copilot-cli alias -- "$0")

# ========================================
# Monalisa Colors for LS
# ========================================
export LS_COLORS="di=38;5;68:ln=38;5;208:so=38;5;197:pi=38;5;221:ex=38;5;154:bd=38;5;240:cd=38;5;240:su=38;5;197:sg=38;5;197:tw=38;5;71:ow=38;5;71:"

# ========================================
# Aliases
# ========================================
alias ls="ls -lah --color=auto"
alias ..="cd .."
alias grep="grep --color=auto"

# ========================================
# History Settings
# ========================================
HISTSIZE=10000
SAVEHIST=10000
HISTFILE=~/.zsh_history
setopt APPEND_HISTORY
Reload shell config: source ~/.bashrc or source ~/.zshrc

----------------------------------------
LunarVim Configuration (~/.config/lvim/config.lua)
----------------------------------------


-- ========================================
-- General Settings
-- ========================================
lvim.format_on_save = true
lvim.lint_on_save = true
lvim.colorscheme = "onedark" -- fallback, we'll override with Monalisa

-- ========================================
-- Key Bindings
-- ========================================
lvim.keys.normal_mode["<C-s>"] = ":w<cr>"
lvim.keys.normal_mode["<C-q>"] = ":q<cr>"
lvim.keys.normal_mode["<leader>ff"] = ":Telescope find_files<cr>"
lvim.keys.normal_mode["<leader>fg"] = ":Telescope live_grep<cr>"

-- ========================================
-- LunarVim UI (Monalisa colors)
-- ========================================
local colors = {
  bg = "#0c0404",
  fg = "#eed45a",
  red = "#a93f22",
  green = "#568354",
  yellow = "#eed45a",
  blue = "#5f563b",
  magenta = "#413c3c",
  cyan = "#414a36",
  white = "#eed45a",
}

lvim.builtin.theme = {
  normal = {
    a = { fg = colors.bg, bg = colors.green },
    b = { fg = colors.fg, bg = colors.bg },
    c = { fg = colors.fg, bg = colors.bg },
  },
  insert = {
    a = { fg = colors.bg, bg = colors.blue },
  },
  visual = {
    a = { fg = colors.bg, bg = colors.magenta },
  },
  replace = {
    a = { fg = colors.bg, bg = colors.red },
  },
  command = {
    a = { fg = colors.bg, bg = colors.yellow },
 },
  terminal = {
    a = { fg = colors.fg, bg = colors.bg },
  },
}

-- ========================================
-- Copilot Settings (Install: :Copilot setup)
-- ========================================
lvim.builtin.copilot = {
  enabled = true,
  filetypes = {
    ["*"] = true,
  },
}

-- ========================================
-- Treesitter & LSP Settings
-- ========================================
lvim.builtin.treesitter.ensure_installed = "all"
lvim.builtin.treesitter.highlight.enabled = true
lvim.lsp.installer.setup.automatic_installation = true
Open LunarVim: lvim > :Copilot setup (follow prompts to set up Copilot)

----------------------------------------
Zellij Configuration (~/.config/zellij/config.yaml)
----------------------------------------
```yaml
========================================
General Settings
========================================
default_shell: /bin/bash # or /bin/zsh
scroll_buffer_size: 10000
copy_command: pbcopy

========================================
Key Bindings
========================================
keybinds:
normal:
- action: [ NewPane, ]
key: [ Alt "n" ]
- action: [ GoToNextTab, ]
key: [ Alt "]" ]
- action: [ GoToPreviousTab, ]
key: [ Alt "[" ]
- action: [ ClosePane, ]
key: [ Alt "q" ]
- action: [ SwitchToMode: "locked" ]
key: [ Alt "l" ]

========================================
Theme (Monalisa colors)
========================================
themes:
default:
fg: "#eed45a"
bg: "#0c0404"
black: "#341809"
red: "#a93f22"
green: "#568354"
yellow: "#eed45a"
blue: "#5f563b"
magenta: "#413c3c"
cyan: "#414a36"
white: "#eed45a"
orange: "#eed45a"

========================================
Layout
========================================
default_layout: compact

========================================
UI
========================================
pane_frames: true
mirror_session: true


**----------------------------------------**
**<a name="atuin"></a> Atuin Configuration (`~/.config/atuin/config.toml`)**
**----------------------------------------**
```toml
# ========================================
# General Settings
# ========================================
dialect = "us"
filter_mode_shell_up_key_binding = true
style = "compact"

# ========================================
# History Settings
# ========================================
history_filter = ["/usr/bin/git", "/usr/bin/lvim"]
max_history_length = 10000

# ========================================
# Sync Settings (optional, for cloud sync)
# ========================================
# [sync]
# host = "https://api.atuin.sh"
# username = "your_username"
# password = "your_password"
----------------------------------------
GitHub Copilot CLI & OpenAI Setup
----------------------------------------

Install GitHub Copilot CLI: npm install -g @githubnext/github-copilot-cli
Setup Copilot CLI: github-copilot-cli auth (follow prompts)
Set OpenAI API Key: export OPENAI_API_KEY="your_key_here" (add to ~/.bashrc or ~/.zshrc)
----------------------------------------
The Fuck & Kitty Terminal Setup

Install The Fuck: pip install thefuck
Add alias (already done in shell configs above): eval $(thefuck --alias)
Install Kitty Terminal: https://sw.kovidgoyal.net/kitty/binary/
Kitty Config (~/.config/kitty/kitty.conf):

# ========================================
# General Settings
# ========================================
font_family      Operator Mono Nerd Font
font_size        10.0
adjust_line_height  0
adjust_column_width 0

# ========================================
# Colors (Monalisa)
# ========================================
background       #0c0404
foreground       #eed45a
cursor           #eed45a
selection_bg     #5f563b
selection_fg     #eed45a

color0           #341809
color1           #a93f22
color2           #568354
color3           #eed45a
color4           #5f563b
color5           #413c3c
color6           #414a36
color7           #eed45a

# ========================================
# Window Settings
# ========================================
remember_window_size  no
initial_window_width   120c
initial_window_height  30c
enabled_layouts       tall,stack,fat

# ========================================
# Tab Bar
# ========================================
tab_bar_style         powerline
tab_powerline_style   round
----------------------------------------
Fonts & Color Scheme

Install Nerd Fonts: https://www.nerdfonts.com/
* Choose Operator Mono Nerd Font (or any Nerd Font you like)
Set Font Size: 10 (as configured in Kitty above)
Color Scheme (Monalisa): Already applied throughout the configs above using these hex codes:
+ #a93f22 (red)
+ #0c0404 (dark bg)
+ #5f563b (brown)
+ #568354 (green)
+ #eed45a (yellow)
+ #341809 (dark brown)
+ #414a36 (dark green)
+ #413c3c (gray)
Final Steps:

Restart all terminals or source the configs.
Test everything:
* Tmux: tmux > prefix + I (install plugins)
* LunarVim: lvim > :Copilot setup
* Zellij: zellij
* Atuin: atuin search
* The Fuck: mistype a command, then fuck
* GitHub Copilot CLI: github-copilot-cli ask "write a bash script to..."
Enjoy your Warp-like, AI-infused terminal ecosystem!
Now, create a command, and watch your AI assistant (Copilot) code, test, and iterate – you're in for a treat!

As a designer and jazz lover, you'll appreciate the mature, elegant look with silver details ( Operator Mono Nerd Font ) and the underlying AI magic. Happy coding!I installed all of them minus Kitty once I have it - can you send me customization for all of them with alll the COOLEST features of each + maximum possible interaction with AIs to look as close as possible to Warp - wihch i love ony 1 thing - i create, he codes, test, change, all by himself... i dont care about all the other features. Im using this color pallete for my other ones - and I like mature look - desinger here, ,jazz lover , details in silver...amd underlying technology - autocomplete - bash that changes - all sorts of super high end stuff -- like the starship demo - fonts from nerd - font size 10 - elegangt - and AI AI AI AI.....Monalisa
Hex color codes: #a93f22, #0c0404, #5f563b, #568354, #eed45a, #341809, #414a36 and #413c3c.



Terminal Customization with AI Focus
Here are customizations for your terminal setup with all the coolest features and maximum AI integration, using your color palette for a mature designer aesthetic.

Alacritty Config

# ~/.config/alacritty/alacritty.yml
window:
  padding: {x: 10, y: 10}
  opacity: 0.95

font:
  normal:
    family: "JetBrainsMono Nerd Font"
  bold:
    family: "JetBrainsMono Nerd Font"
    style: Bold
  size: 10.0

colors:
  primary:
    background: '#0c0404'
    foreground: '#eed45a'
  cursor:
    text: '#0c0404'
    cursor: '#eed45a'
  normal:
    black: '#0c0404'
    red: '#a93f22'
    green: '#568354'
    yellow: '#eed45a'
    blue: '#5f563b'
    magenta: '#341809'
    cyan: '#414a36'
    white: '#413c3c'
Starship Prompt

# ~/.config/starship.toml
format = """
$username\
$directory\
$git_branch\
$git_status\
$line_break\
$character"""

[character]
success_symbol = "[❯](bold #eed45a)"
error_symbol = "[❯](bold #a93f22)"

[directory]
style = "bold #568354"

[git_branch]
symbol = " "
style = "bold #5f563b"
Zsh with AI Features

# ~/.zshrc
# Oh My Zsh setup
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME=""
plugins=(git zsh-autosuggestions zsh-syntax-highlighting fzf copilot thefuck)
source $ZSH/oh-my-zsh.sh

# Modern CLI tools
alias ls="exa --icons --group-directories-first"
alias cat="bat --theme=base16"
alias grep="rg"

# Initialize Starship prompt
eval "$(starship init zsh)"

# GitHub Copilot CLI for terminal AI assistance
eval "$(github-copilot-cli alias -- "$0")"

# AI Command Assistant
aicommand() {
  local cmd=$(curl -s "https://api.openai.com/v1/completions" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d "{
      \"model\": \"text-davinci-003\",
      \"prompt\": \"Convert this English to a bash command: $1\",
      \"max_tokens\": 100
    }" | jq -r '.choices[0].text' | tr -d '\n')
  
  echo "Command: $cmd"
  read -p "Execute? (y/n) " choice
  case "$choice" in
    y|Y ) eval "$cmd";;
    * ) echo "Command not executed";;
  esac
}
alias ai="aicommand"

# Autosuggestion styling
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=#5f563b"
Kitty Terminal Config

# ~/.config/kitty/kitty.conf
font_family      JetBrainsMono Nerd Font
bold_font        JetBrainsMono Nerd Font Bold
italic_font      JetBrainsMono Nerd Font Italic
font_size 10.0

window_padding_width 10
background_opacity 0.95
dynamic_background_opacity yes

# Color scheme
background            #0c0404
foreground            #eed45a
cursor                #eed45a
selection_background  #341809

# Regular colors
color0                #0c0404
color1                #a93f22
color2                #568354
color3                #eed45a
color4                #5f563b
color5                #341809
color6                #414a36
color7                #413c3c

# Enable AI integration
allow_remote_control yes
shell_integration enabled

# Keyboard shortcuts for AI features
map ctrl+shift+a kitten hints --type=linenum
Neovim with AI Coding

-- ~/.config/nvim/init.lua
-- Install packer first, then add:

require('packer').startup(function(use)
  use 'wbthomason/packer.nvim'
  
  -- AI coding assistance
  use 'github/copilot.vim'
  use 'zbirenbaum/copilot.lua'
  use 'zbirenbaum/copilot-cmp'
  
  -- Completions and LSP
  use 'neovim/nvim-lspconfig'
  use 'hrsh7th/nvim-cmp'
  use 'hrsh7th/cmp-nvim-lsp'
end)

-- Custom jazz-inspired color scheme
vim.cmd([[
  highlight Normal guibg=#0c0404 guifg=#eed45a
  highlight LineNr guifg=#5f563b
  highlight CursorLine guibg=#341809
  highlight Statement guifg=#a93f22
  highlight Identifier guifg=#568354
]])

-- Copilot configuration
vim.g.copilot_no_tab_map = true
vim.api.nvim_set_keymap("i", "<C-J>", 'copilot#Accept("<CR>")', { silent = true, expr = true })
vim.api.nvim_set_keymap("i", "<C-H>", 'copilot#Previous()', { silent = true, expr = true })
vim.api.nvim_set_keymap("i", "<C-L>", 'copilot#Next()', { silent = true, expr = true })

-- Enhanced Copilot setup
require('copilot').setup({
  suggestion = {
    auto_trigger = true,
    keymap = {
      accept = "<C-j>",
      accept_word = "<C-k>",
      accept_line = "<C-l>",
    },
  },
})
Tmux Configuration

# ~/.tmux.conf
# Set prefix key
unbind C-b
set -g prefix C-Space

# Enable mouse support
set -g mouse on

# Custom status bar with your color palette
set -g status-style "bg=#0c0404,fg=#eed45a"
set -g status-left "#[fg=#0c0404,bg=#eed45a,bold] #S "
set -g window-status-current-format "#[fg=#0c0404,bg=#568354] #I #W "

# Pane borders
set -g pane-border-style "fg=#414a36"
set -g pane-active-border-style "fg=#568354"

# Plugins for enhanced functionality
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-resurrect'
set -g @plugin 'sainnhe/tmux-fzf'
AI Assistance Tools to Install
GitHub Copilot CLI: npm install -g @githubnext/github-copilot-cli
Fig: For enhanced autocomplete that feels AI-like: https://fig.io/
Warp AI Compatible Tools:
Install thefuck for command correction: pip install thefuck
Set up OpenAI API key for command generation: export OPENAI_API_KEY="your-key"
Extra Enhancements
For a fully integrated AI experience similar to Warp:

Install LunarVim for an IDE-like experience with Copilot built-in
Set up Zellij (alternative to tmux with more modern features)
Install atuin for AI-searchable shell history
Would you like me to explain or break down any of these configurations in more detail?



I need a very very robust enterprise grade script with verbose fall backs, separated in blocks -------, and all the ultimate quality to create a similar warp terrminal - and with the Monalisa colors -
