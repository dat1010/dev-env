# dev-env

Bootstrap scripts for setting up a Linux dev environment.

## Usage

**Install tools** (runs all scripts in `runs/`):
```bash
./run
./run neovim   # run only scripts matching "neovim"
./run --dry    # preview without executing
```

**Deploy configs** (copies `.config/` to `$XDG_CONFIG_HOME`):
```bash
./dev-env
./dev-env --dry
```

## What gets installed

| Script | What it does |
|---|---|
| `runs/neovim` | Installs Neovim from pre-built release, pulls nvim config from a configurable git repo |
| `runs/oh-my-zsh` | Installs zsh + Oh My Zsh |
| `runs/asdf` | Installs asdf version manager |

## Changing the Neovim config repo

Edit the variables at the top of `runs/neovim`:

```bash
NVIM_CONFIG_REPO="https://github.com/dat1010/configFiles"
NVIM_CONFIG_SUBDIR="nvim"  # set to "" if config is at repo root
```

## Overriding the Neovim version

```bash
NVIM_VERSION=v0.10.0 ./runs/neovim
```
