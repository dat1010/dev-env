# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

A dotfiles/dev environment bootstrap repo. It manages shell config (`.zshrc`), Neovim config (`.config/nvim/`), and installation scripts for tools like Neovim and Oh My Zsh.

## Key Scripts

- **`dev-env`** — Copies `.config/` directories and `.specialconfig` into the system config locations (`$XDG_CONFIG_HOME` and `$HOME`). Uses `gfind` (GNU find via `brew install findutils` on macOS).
- **`run`** — Iterates over executable scripts in `runs/` and executes them. Supports a positional filter argument and `--dry` flag for dry runs.

### Usage

```bash
# Copy configs to system locations
./dev-env
./dev-env --dry        # preview without making changes

# Run all install scripts
./run
./run neovim           # run only scripts matching "neovim"
./run --dry            # preview without executing

# Run a specific install script directly
./runs/neovim
./runs/oh-my-zsh
```

## Architecture

```
.
├── dev-env            # Config deployment script (copies .config/ → $XDG_CONFIG_HOME)
├── run                # Install script runner (executes scripts in runs/)
├── runs/              # Individual tool install scripts (must be executable)
│   ├── neovim         # Builds Neovim from source (targets Linux via apt)
│   └── oh-my-zsh      # Installs zsh + Oh My Zsh (targets Linux via apt)
├── .config/
│   └── nvim/          # Neovim config using lazy.nvim plugin manager
│       ├── init.lua   # Entry point: options, keymaps, lazy.nvim bootstrap
│       └── lua/
│           ├── plugins.lua         # Base plugins (vim-sleuth, Comment.nvim)
│           └── plugins/            # Per-plugin config files loaded by lazy.nvim
└── .zshrc             # Oh My Zsh shell config with aliases, asdf, nvm, direnv
```

## Neovim Config

- Plugin manager: **lazy.nvim** (auto-installed on first launch)
- Plugins are split: `lua/plugins.lua` for base plugins, `lua/plugins/<name>.lua` for individual plugin configs
- Leader key: `<Space>`
- To add a new plugin, create a new file in `.config/nvim/lua/plugins/` returning a lazy.nvim spec table

## macOS vs Linux

The `run` and `dev-env` scripts use `gfind` (GNU find) — on macOS this requires `brew install findutils`. The `runs/neovim` and `runs/oh-my-zsh` scripts use `apt` and are intended for Linux targets.
