---
title: "SERVIDOR DE CORREO LINUX (Postfix + Dovecot + SSL)"
description: Configurar un servidor de correo en Linux con Postfix y Dovecot, permitiendo envío interno y externo de correos con seguridad SSL/TLS.
pubDatetime: 2026-01-18T10:00:00Z
tags:
  - postfix
  - dovecot
  - linux
  - thunderbird
  - virtualbox
draft: false
---

Implementación de un servidor de correo electrónico sobre Linux utilizando Postfix y Dovecot. El proyecto incluye la configuración de servicios SMTP e IMAP, gestión de usuarios locales, cifrado SSL/TLS y pruebas de comunicación entre cuentas para comprender el funcionamiento de una infraestructura de correo empresarial.


## Table of contents

## Shell: Instalación de servicios

Antes de instalar cualquier servicio, se actualizaron los repositorios de Ubuntu para garantizar que los paquetes descargados fueran las versiones más recientes disponibles.

```bash
sudo apt update
sudo apt install postfix dovecot-imapd dovecot-pop3d mailutils
```
<figure>
  <img
    src="/Terminal.png"
    alt="Abstract diagram of interconnected neural networks"
  />
  <figcaption class="text-center">
    AI agents chain reasoning and action in autonomous loops.
  </figcaption>
</figure>









## Classic tool replacements

### `ls` → `eza` (formerly `exa`)

```bash
eza --tree --level=2 --icons --git    # tree with icons and Git status
eza -la --sort=modified               # long list, sorted by date
```

### `find` → `fd`

```bash
# find: verbose and poor ergonomics
find . -name "*.ts" -not -path "*/node_modules/*"    # [!code --]

# fd: intuitive, respects .gitignore by default
fd -e ts                    # all .ts in the project          # [!code ++]
fd -e ts --exec bat {}      # open each result with bat       # [!code ++]
```

### `grep` → `ripgrep` (`rg`)

```bash
# classic grep
grep -r "useEffect" src/ --include="*.tsx"      # [!code --]

# rg: 5-10× faster, respects .gitignore
rg "useEffect" --type ts                         # [!code ++]
rg "TODO|FIXME|HACK" --type ts --stats           # [!code ++]
rg "deprecated" -l                               # filenames only # [!code ++]
```

### `cat` → `bat`

`bat` is `cat` with syntax highlighting, line numbers, paging, and built-in Git diff:

```bash
bat src/components/Header.astro     # with colors and lines
bat --diff file.ts                  # shows inline Git changes
```

### `cd` → `zoxide`

It learns which directories you visit frequently and lets you jump to them with a few letters:

```bash
z astro      # jumps to ~/projects/my-astro-blog if it's the most visited
z blog src   # multiple match
zi           # interactive mode with fzf
```

## Multiplexer: `tmux` with modern config

```bash file=~/.tmux.conf
# More comfortable prefix
set -g prefix C-a
unbind C-b

# Split panes with intuitive keys
bind | split-window -h -c "#{pane_current_path}"  # [!code highlight]
bind - split-window -v -c "#{pane_current_path}"  # [!code highlight]

# Navigation with Alt+arrow (no prefix)
bind -n M-Left  select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up    select-pane -U
bind -n M-Down  select-pane -D

# Mouse enabled
set -g mouse on

# 256 colors
set -g default-terminal "tmux-256color"
```

## Fuzzy finder: `fzf` — the multiplier of everything

`fzf` turns any list into an interactive finder. Just add `| fzf` to any command.

```bash
# Search in command history
CTRL+R with integrated fzf

# Checkout branch with preview
git branch | fzf --preview 'git log --oneline {}' | xargs git checkout

# Kill processes
ps aux | fzf --multi | awk '{print $2}' | xargs kill

# Find and open file
fd -e ts | fzf --preview 'bat --color=always {}' | xargs nvim
```

## Modern Git: `lazygit`

A Git TUI (Terminal UI) that makes it obvious what's happening in your repository:

```bash
lazygit   # opens the interface
```

Standout features:

- View diffs by file and by line
- Selective stage (individual lines, not just files)
- Resolve conflicts visually
- Interactive rebase with drag & drop

## My optimized basic `.zshrc`

```bash file=~/.zshrc
# Fast load with lazy loading
export PATH="$HOME/.cargo/bin:$HOME/.local/bin:$PATH"

# Modern aliases
alias ls='eza --icons'
alias ll='eza -la --icons --git'
alias tree='eza --tree --icons'
alias cat='bat'
alias find='fd'
alias grep='rg'
alias lg='lazygit'

# fzf integration
source <(fzf --zsh)

# zoxide
eval "$(zoxide init zsh)"

# starship
eval "$(starship init zsh)"
```

> The best time investment in terminal productivity is not learning new tools — it's mastering the ones you already have. But when a modern tool does the same thing 5× faster with better DX, the switch pays for itself in the first week.
