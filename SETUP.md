# Neovim Setup Guide

A comprehensive guide to my Neovim configuration, based on kickstart.nvim with customizations for Python and Go development.

---

## Table of Contents

1. [Quick Start (New Machine Setup)](#quick-start-new-machine-setup)
2. [Prerequisites](#prerequisites)
3. [Configuration Overview](#configuration-overview)
4. [Plugins](#plugins)
5. [Keybindings Reference](#keybindings-reference)
6. [Language Support](#language-support)
7. [Customizations Made](#customizations-made)
8. [Common Workflows](#common-workflows)
9. [Troubleshooting](#troubleshooting)
10. [Future Additions](#future-additions)

---

## Quick Start (New Machine Setup)

Run these commands to replicate this setup on a new machine:

```bash
# 1. Install Neovim (macOS)
brew install neovim

# 2. Install iTerm2 (required for true color support)
brew install --cask iterm2

# 3. Install a Nerd Font (for icons)
brew install --cask font-jetbrains-mono-nerd-font

# 4. Install dependencies and linters
brew install ripgrep fd ruff golangci-lint markdownlint-cli

# 5. Clone your config (replace with your repo if you back this up)
git clone https://github.com/nvim-lua/kickstart.nvim.git ~/.config/nvim

# 6. Create Python venv for Neovim provider
python3 -m venv ~/.config/nvim/venv
~/.config/nvim/venv/bin/pip install pynvim

# 7. Launch Neovim (plugins auto-install on first run)
nvim
```

**Post-install:**
- Set iTerm2 font: Settings → Profiles → Text → Font → "JetBrainsMono Nerd Font"
- Press `q` to close the Lazy plugin installer window
- Run `:checkhealth` to verify everything is working
- Run `:Mason` to verify language servers and debug adapters are installed

---

## Prerequisites

| Requirement | Purpose | Install Command |
|-------------|---------|-----------------|
| Neovim 0.11+ | Editor | `brew install neovim` |
| iTerm2 | True color support | `brew install --cask iterm2` |
| Nerd Font | Icons in file tree | `brew install --cask font-jetbrains-mono-nerd-font` |
| Go | Go development | `brew install go` |
| Python 3 | Python development | Comes with macOS / `brew install python` |
| ripgrep | Fast searching | `brew install ripgrep` |
| fd | Fast file finding | `brew install fd` |
| ruff | Python linter | `brew install ruff` |
| golangci-lint | Go linter | `brew install golangci-lint` |
| markdownlint | Markdown linter | `brew install markdownlint-cli` |

---

## Configuration Overview

| File | Purpose |
|------|---------|
| `~/.config/nvim/init.lua` | Main configuration file (everything lives here) |
| `~/.config/nvim/lua/kickstart/plugins/` | Optional plugin configs (debug, lint, autopairs, etc.) |
| `~/.config/nvim/venv/` | Python virtual environment for Neovim |
| `~/.local/share/nvim/` | Plugin data, Mason installs |
| `~/.local/state/nvim/` | Shada, undo history |
| `~/.cache/nvim/` | Cache files |

### Key Settings

```lua
vim.g.mapleader = ' '              -- Leader key is Space
vim.g.have_nerd_font = true        -- Enable Nerd Font icons
vim.g.python3_host_prog = '~/.config/nvim/venv/bin/python'  -- Python provider
vim.o.termguicolors = true         -- True color support
vim.o.number = true                -- Line numbers
vim.o.relativenumber = false       -- Relative line numbers (disabled)
vim.o.mouse = 'a'                  -- Mouse support
vim.o.clipboard = 'unnamedplus'    -- System clipboard integration
vim.o.undofile = true              -- Persistent undo
vim.o.ignorecase = true            -- Case-insensitive search
vim.o.smartcase = true             -- ...unless uppercase used
vim.o.signcolumn = 'yes'           -- Always show sign column
vim.o.cursorline = true            -- Highlight current line
```

---

## Plugins

### Core Plugins

| Plugin | Purpose | Key Features |
|--------|---------|--------------|
| **lazy.nvim** | Plugin manager | Fast, lazy-loading |
| **telescope.nvim** | Fuzzy finder | Find files, grep, buffers |
| **nvim-treesitter** | Syntax highlighting | Better code colors, parsing |
| **nvim-lspconfig** | LSP support | Code intelligence |
| **mason.nvim** | LSP/tool installer | Auto-install language servers |
| **blink.cmp** | Autocompletion | Fast, modern completion |
| **conform.nvim** | Formatting | Auto-format on save |

### UI Plugins

| Plugin | Purpose |
|--------|---------|
| **neo-tree.nvim** | File tree sidebar |
| **which-key.nvim** | Keybinding hints |
| **tokyonight.nvim** | Color scheme |
| **fidget.nvim** | LSP progress indicator |
| **nvim-web-devicons** | File icons |
| **mini.nvim** | Statusline, surround, and more |
| **todo-comments.nvim** | Highlight TODO/FIXME/etc |
| **indent-blankline.nvim** | Indent guides |
| **render-markdown.nvim** | Pretty markdown rendering |

### Navigation & Editing

| Plugin | Purpose |
|--------|---------|
| **harpoon** | Quick file bookmarks |
| **gitsigns.nvim** | Git integration in gutter |
| **guess-indent.nvim** | Auto-detect indentation |
| **nvim-autopairs** | Auto-close brackets, quotes |
| **auto-save.nvim** | Auto-save files |

### Debugging & Testing

| Plugin | Purpose |
|--------|---------|
| **nvim-dap** | Debug Adapter Protocol client |
| **nvim-dap-ui** | Debugger UI |
| **nvim-dap-go** | Go debugging (delve) |
| **nvim-dap-python** | Python debugging (debugpy) |
| **neotest** | Test runner framework |
| **neotest-python** | Python test adapter |
| **neotest-golang** | Go test adapter |

### Diagnostics & Linting

| Plugin | Purpose |
|--------|---------|
| **trouble.nvim** | Pretty diagnostics list |
| **nvim-lint** | Additional linting |

### Language-Specific

| Plugin | Purpose |
|--------|---------|
| **lazydev.nvim** | Lua/Neovim development |
| **LuaSnip** | Snippet engine |

---

## Keybindings Reference

**Leader key: `Space`**

### Essential Navigation

| Keybinding | Action | Context |
|------------|--------|---------|
| `Space sf` | Search files | Find any file |
| `Space sg` | Search by grep | Search file contents |
| `Space s.` | Recent files | Previously opened files |
| `Space Space` | Switch buffers | Open files |
| `Space /` | Search in current file | Fuzzy find in buffer |
| `Space sk` | Search keymaps | Find any keybinding |
| `Space sh` | Search help | Neovim documentation |

### File Tree (Neo-tree)

| Keybinding | Action |
|------------|--------|
| `\` | Toggle file tree |
| `Enter` | Open file |
| `a` | Add file/folder |
| `d` | Delete |
| `r` | Rename |
| `c` | Copy |
| `m` | Move |
| `H` | Toggle hidden files |
| `?` | Show help |

### Harpoon (Quick File Switching)

| Keybinding | Action |
|------------|--------|
| `Space a` | Add file to Harpoon |
| `Ctrl+e` | Open Harpoon menu |
| `Space 1` | Jump to file 1 |
| `Space 2` | Jump to file 2 |
| `Space 3` | Jump to file 3 |
| `Space 4` | Jump to file 4 |

### Code/LSP

| Keybinding | Action |
|------------|--------|
| `grd` | Go to definition |
| `grr` | Find references |
| `gri` | Go to implementation |
| `grt` | Go to type definition |
| `K` | Hover documentation |
| `Space ca` | Code actions |
| `Space rn` | Rename symbol |
| `gO` | Document symbols |
| `gW` | Workspace symbols |

### Debugging (nvim-dap)

| Keybinding | Action |
|------------|--------|
| `F5` | Start/Continue debugging |
| `F1` | Step into |
| `F2` | Step over |
| `F3` | Step out |
| `F7` | Toggle debugger UI |
| `Space b` | Toggle breakpoint |
| `Space B` | Set conditional breakpoint |

### Testing (Neotest)

| Keybinding | Action |
|------------|--------|
| `Space tt` | Run nearest test |
| `Space tf` | Run all tests in file |
| `Space ts` | Toggle test summary |
| `Space to` | Show test output |
| `Space tO` | Toggle output panel |
| `Space td` | Debug nearest test |

### Diagnostics (Trouble)

| Keybinding | Action |
|------------|--------|
| `Space xx` | Toggle all diagnostics |
| `Space xX` | Toggle buffer diagnostics |
| `Space cs` | Toggle symbols |
| `Space xL` | Toggle location list |
| `Space xQ` | Toggle quickfix list |
| `[d` | Previous diagnostic |
| `]d` | Next diagnostic |
| `Space q` | Open diagnostic quickfix |
| `Space sd` | Search all diagnostics |

### Window Management

| Keybinding | Action |
|------------|--------|
| `Ctrl+h` | Move to left window |
| `Ctrl+l` | Move to right window |
| `Ctrl+j` | Move to lower window |
| `Ctrl+k` | Move to upper window |
| `Ctrl+w s` | Horizontal split |
| `Ctrl+w v` | Vertical split |
| `Ctrl+w q` | Close window |

### Terminal

| Keybinding | Action |
|------------|--------|
| `:term` | Open terminal |
| `Space r` | Run current file (Python/Go) |
| `Esc Esc` | Exit terminal mode |

### Git (Gitsigns)

| Keybinding | Action |
|------------|--------|
| `]c` | Next hunk |
| `[c` | Previous hunk |
| `Space hs` | Stage hunk |
| `Space hr` | Reset hunk |
| `Space hp` | Preview hunk |
| `Space hb` | Blame line |

### General

| Keybinding | Action |
|------------|--------|
| `Esc` | Clear search highlight |
| `:w` | Save file |
| `:q` | Quit |
| `:wq` | Save and quit |
| `u` | Undo |
| `Ctrl+r` | Redo |
| `Space as` | Toggle auto-save on/off |

---

## Language Support

### Python

**LSP:** Pyright (auto-installed via Mason)

**Linter:** Ruff (via nvim-lint)

**Debugger:** debugpy (auto-installed via Mason)

**Test Runner:** pytest (via neotest-python)

**Features:**
- Type checking & autocompletion
- Go to definition / Find references
- Hover documentation
- Diagnostics & linting
- Debugging with breakpoints
- Test running & debugging

**Treesitter:** `python` parser installed

**Run file:** `Space r` runs current Python file

**Debug:**
1. Set breakpoint: `Space b`
2. Start debugging: `F5`
3. Step through: `F1` (into), `F2` (over), `F3` (out)
4. Toggle UI: `F7`

**Run tests:**
- `Space tt` - Run test under cursor
- `Space tf` - Run all tests in file
- `Space td` - Debug test under cursor

### Go

**LSP:** gopls (auto-installed via Mason)

**Linter:** golangci-lint (via nvim-lint)

**Debugger:** delve (auto-installed via Mason)

**Test Runner:** go test (via neotest-golang)

**Features:**
- Full language support
- Autocompletion
- Go to definition / Find references
- Formatting & imports management
- Debugging with breakpoints
- Test running & debugging

**Treesitter:** `go`, `gomod`, `gosum` parsers installed

**Run file:** `Space r` runs current Go file

### Lua

**LSP:** lua_ls (auto-installed for Neovim config editing)

---

## Customizations Made

Changes from base kickstart.nvim:

### 1. Python Provider
```lua
vim.g.python3_host_prog = vim.fn.expand('~/.config/nvim/venv/bin/python')
```

### 2. True Color Support
```lua
vim.o.termguicolors = true
```

### 3. Nerd Font Enabled
```lua
vim.g.have_nerd_font = true
```

### 4. LSP Servers Enabled
```lua
local servers = {
  gopls = {},
  pyright = {},
  lua_ls = { ... },
}
```

### 5. Treesitter Languages
```lua
ensure_installed = { 'bash', 'c', 'diff', 'go', 'gomod', 'gosum', 'html', 'lua', 'luadoc', 'markdown', 'markdown_inline', 'python', 'query', 'vim', 'vimdoc' }
```

### 6. Enabled Kickstart Plugins
- `kickstart.plugins.debug` - Debugging (nvim-dap)
- `kickstart.plugins.indent_line` - Indent guides
- `kickstart.plugins.lint` - Linting (nvim-lint)
- `kickstart.plugins.autopairs` - Auto-close brackets
- `kickstart.plugins.neo-tree` - File tree

### 7. Added Plugins
- **Harpoon** - Quick file navigation with `Space 1-4`
- **Trouble.nvim** - Better diagnostics UI
- **Neotest** - Test runner with Python/Go adapters
- **render-markdown.nvim** - Pretty markdown viewing

### 8. Debug Config (lua/kickstart/plugins/debug.lua)
Added Python debugging support:
```lua
-- Debuggers installed
ensure_installed = { 'delve', 'debugpy' }

-- Python setup
require('dap-python').setup(vim.fn.expand('~/.config/nvim/venv/bin/python'))
```

### 9. Lint Config (lua/kickstart/plugins/lint.lua)
Added Python and Go linters:
```lua
lint.linters_by_ft = {
  markdown = { 'markdownlint' },
  python = { 'ruff' },
  go = { 'golangcilint' },
}
```

### 10. Run File Keymap
```lua
vim.keymap.set('n', '<leader>r', function()
  local ft = vim.bo.filetype
  if ft == 'python' then
    vim.cmd('split | term python3 ' .. vim.fn.expand('%'))
  elseif ft == 'go' then
    vim.cmd('split | term go run ' .. vim.fn.expand('%'))
  end
end, { desc = '[R]un current file' })
```

---

## Common Workflows

### Opening a Project
```bash
cd ~/dev/myproject
nvim .
```
Then press `\` to see file tree, or `Space sf` to find files.

### Working with Multiple Files
1. Open first file
2. `Space a` to add to Harpoon
3. Open second file, `Space a` again
4. Now `Space 1` and `Space 2` switch instantly between them

### Finding Code
- `Space sg` → type search term → see results across all files
- `Space sw` → search for word under cursor

### Code Navigation
- `grd` → jump to where function/variable is defined
- `grr` → see everywhere it's used
- `K` → see documentation popup

### Running Code
- Edit your file
- `Space r` → runs in split terminal
- `Esc Esc` → exit terminal mode
- `Ctrl+w q` → close terminal split

### Debugging Python/Go
1. Open your file
2. `Space b` → set breakpoint on a line
3. `F5` → start debugging
4. Use `F1/F2/F3` to step through code
5. `F7` → toggle debugger UI to see variables
6. `F5` again to continue to next breakpoint

### Running Tests
1. Open a test file (e.g., `test_main.py` or `main_test.go`)
2. `Space tt` → run test under cursor
3. `Space ts` → toggle test summary panel
4. `Space to` → see test output
5. `Space td` → debug a failing test

### Viewing Diagnostics
- `Space xx` → open Trouble with all diagnostics
- `[d` / `]d` → jump between diagnostic messages
- Hover over error → `K` for details

### Git Workflow
- See changes in gutter (green = added, red = removed)
- `Space hp` → preview what changed in a hunk
- `Space hs` → stage hunk
- Use `git commit` in terminal

### Viewing Markdown
- Open any `.md` file
- render-markdown.nvim automatically renders headings, lists, code blocks nicely
- Toggle with `:RenderMarkdown toggle`

---

## Troubleshooting

### Icons show as "?" or boxes
- Install a Nerd Font: `brew install --cask font-jetbrains-mono-nerd-font`
- Set it in iTerm2: Settings → Profiles → Text → Font

### Colors look wrong
- Use iTerm2 (Apple Terminal doesn't support true colors)
- Ensure `vim.o.termguicolors = true` is in config

### LSP not working
1. Run `:checkhealth` to diagnose
2. Run `:Mason` to see installed language servers
3. Ensure the server is installed (e.g., `pyright`, `gopls`)

### Debugger not working
1. Run `:Mason` and verify `debugpy` and `delve` are installed
2. For Python: ensure your venv has debugpy or use the nvim venv
3. Check `:DapShowLog` for errors

### Tests not running
1. Ensure test file follows naming convention (`test_*.py` or `*_test.go`)
2. Run `:Neotest summary` to see detected tests
3. Check that pytest/go is available in your PATH

### Linting errors not showing
1. Ensure linters are installed: `ruff`, `golangci-lint`, `markdownlint`
2. Run `:LintInfo` to see active linters

### Python provider errors
1. Ensure venv exists: `ls ~/.config/nvim/venv`
2. Reinstall pynvim: `~/.config/nvim/venv/bin/pip install pynvim`

### Plugins not loading
1. Run `:Lazy` to see plugin status
2. Press `U` to update all plugins
3. Restart Neovim

### "No such file" when running `:Tutor`
Run `:Lazy sync` then restart Neovim

---

## Future Additions

Plugins to consider adding:

| Plugin | Purpose | Priority |
|--------|---------|----------|
| `copilot.vim` | AI completion | Optional |
| `diffview.nvim` | Better git diff view | Low |
| `neogit` | Git UI inside Neovim | Low |
| `nvim-spectre` | Search and replace across files | Low |

---

## Useful Commands

| Command | Action |
|---------|--------|
| `:Lazy` | Open plugin manager |
| `:Mason` | Open LSP/tool installer |
| `:checkhealth` | Diagnose issues |
| `:Tutor` | Interactive Vim tutorial |
| `:help <topic>` | Get help on anything |
| `:TSInstall <lang>` | Install treesitter parser |
| `:LspInfo` | See active LSP servers |
| `:ConformInfo` | See active formatters |
| `:Trouble` | Open diagnostics panel |
| `:Neotest summary` | Open test summary |
| `:RenderMarkdown toggle` | Toggle markdown rendering |

---

## Windows (WSL) Setup

Complete instructions for replicating this setup on Windows with WSL.

### Step 1: Install WSL (if not already installed)

Open PowerShell as Administrator:
```powershell
wsl --install
```

Restart your computer, then open Ubuntu from the Start menu to complete setup.

### Step 2: Install a Nerd Font on Windows

Download and install a Nerd Font on **Windows** (not WSL):

1. Go to https://www.nerdfonts.com/font-downloads
2. Download "JetBrainsMono Nerd Font"
3. Extract the zip
4. Select all `.ttf` files → Right-click → "Install for all users"

### Step 3: Install Windows Terminal (Recommended)

1. Install from Microsoft Store: "Windows Terminal"
2. Open Windows Terminal → Settings (`Ctrl+,`)
3. Select your Ubuntu profile → Appearance
4. Set Font face to "JetBrainsMono Nerd Font"
5. Enable "Use acrylic material" (optional, for transparency)

### Step 4: Install Dependencies in WSL

Open WSL/Ubuntu terminal:

```bash
# Update packages
sudo apt update && sudo apt upgrade -y

# Install Neovim (latest)
sudo add-apt-repository ppa:neovim-ppa/unstable -y
sudo apt update
sudo apt install neovim -y

# Install build essentials and dependencies
sudo apt install -y build-essential git curl wget unzip ripgrep fd-find

# Fix fd command name (Ubuntu names it fdfind)
sudo ln -s $(which fdfind) /usr/local/bin/fd

# Install Python and pip
sudo apt install -y python3 python3-pip python3-venv

# Install Go
sudo apt install -y golang-go

# Or for latest Go:
# wget https://go.dev/dl/go1.22.0.linux-amd64.tar.gz
# sudo tar -C /usr/local -xzf go1.22.0.linux-amd64.tar.gz
# Add to ~/.bashrc: export PATH=$PATH:/usr/local/go/bin

# Install Node.js (needed for some LSPs)
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs

# Install linters
pip3 install --user ruff
go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest
sudo npm install -g markdownlint-cli

# Install uv (Python package manager)
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Step 5: Clone Your Neovim Config

```bash
# If you've backed up your config to GitHub:
git clone git@github.com:YOUR_USERNAME/nvim-config.git ~/.config/nvim

# Or clone fresh kickstart and apply your customizations:
git clone https://github.com/nvim-lua/kickstart.nvim.git ~/.config/nvim
```

### Step 6: Create Python venv for Neovim

```bash
python3 -m venv ~/.config/nvim/venv
~/.config/nvim/venv/bin/pip install pynvim
```

### Step 7: Set up Environment Variables

Add to your `~/.bashrc` or `~/.zshrc`:

```bash
# Go path
export PATH=$PATH:$HOME/go/bin

# Local bin (for pip --user installs)
export PATH=$PATH:$HOME/.local/bin

# Neovim as default editor
export EDITOR=nvim
export VISUAL=nvim
```

Then reload:
```bash
source ~/.bashrc
```

### Step 8: Launch Neovim

```bash
nvim
```

- Wait for plugins to install
- Press `q` to close Lazy window
- Run `:checkhealth` to verify everything works
- Run `:Mason` to verify LSPs install

### WSL-Specific Tips

**Clipboard Integration:**

Your config already has `clipboard = 'unnamedplus'`. For this to work with Windows clipboard:

```bash
# Install win32yank for clipboard support
curl -sLo /tmp/win32yank.zip https://github.com/equalsraf/win32yank/releases/latest/download/win32yank-x64.zip
unzip -p /tmp/win32yank.zip win32yank.exe > /tmp/win32yank.exe
chmod +x /tmp/win32yank.exe
sudo mv /tmp/win32yank.exe /usr/local/bin/
```

**Accessing Windows Files:**

```bash
# Windows C: drive is mounted at /mnt/c
cd /mnt/c/Users/YourName/Documents
```

**Opening Files from Windows Explorer:**

Add to your Windows Terminal profile (Settings → Ubuntu → Command line):
```
wsl.exe -d Ubuntu
```

### Windows Terminal Keybindings

To avoid conflicts with Neovim, you may want to unbind some Windows Terminal defaults:

1. Open Windows Terminal Settings → Actions
2. Remove or rebind:
   - `Ctrl+V` (conflicts with visual block)
   - `Ctrl+C` (can conflict)

### Quick Verification Checklist

Run these in WSL to verify setup:

```bash
nvim --version          # Should show 0.10+
go version              # Should show Go
python3 --version       # Should show Python 3
ruff --version          # Linter
node --version          # Node.js
git --version           # Git
which fd                # fd finder
which rg                # ripgrep
```

### Syncing Config Between Mac and Windows

**Option 1: Git Repository (Recommended)**

Keep your config in a git repo and pull on both machines:

```bash
# On Mac (after making changes)
cd ~/.config/nvim
git add -A
git commit -m "Update config"
git push

# On Windows/WSL
cd ~/.config/nvim
git pull
```

**Option 2: Dotfiles Manager**

Use a tool like `chezmoi` or `stow` to manage dotfiles across machines.

---

## Backup Your Config

To back up this configuration to a git repository:

```bash
cd ~/.config/nvim
git remote set-url origin git@github.com:YOUR_USERNAME/nvim-config.git
git add -A
git commit -m "My neovim config"
git push
```

To restore on a new machine:
```bash
git clone git@github.com:YOUR_USERNAME/nvim-config.git ~/.config/nvim
```

---

*Last updated: December 2024*
