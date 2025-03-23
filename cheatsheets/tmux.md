# Tmux

## Session Management

- `tmux new -s mysession`:  start new session named *mysession*
- `tmux ls              `:  list sessions 
- `tmux a               `:  attach to last session
- `tmux a -t mysession  `:  attach to session named *mysession*
- `tmux kill-sess -t my `:  kill session named *my*

## Commands

```bash
# Show tmux sessions
tmux list-sessions

# Attach to last session
tmux attach-session

# Kill session
tmux kill-session -t hello

# Default prefix key (short pre): CTRL+b
# New horizontal pane: pre + "
# Close pane: C+d or "exit"

# Command prompt: pre + :, then type command like "split-window"
# you can do all via prompt or keystroke

# Config is in
vim ~/.tmux.conf

# Split vertical:   pre + v
# Split horizontal: pre + h
# Go to pane:       pre + arrow key
# Resize pane:      pre + alt + arrow key
# Close pane:       pre + x

# New window:       pre + w
# Rename window:    pre + n
# Go to window:     pre + 1..n
# Next/prev window: alt + right/lefv

## EXTRACTO: better copy mode
# Search output:    pre + tab
# Insert selecte:   tab

## COPY MODE
# Copy mode:        pre + [
# Scroll up/down:   ctr + u/d
# Search:           /
# Start selection:  v
# Copy selection:   y (yank)
# Leave copy mode:  q
# Paste:            pre + ]; ctr + sh + v
# File search:      pre + ctr + f
# Git status files: pre + ctr + g
# Url search:       pre + ctr + u
# Number search:    pre + ctr + d
# IP address s.:    pre + alt + i
# Next/Prev result: n, N

## tmuxp Session Management
tmuxp load fabric

# create sessions with yaml files
vim ~/.tmuxp/fabric.yaml

# examples
open https://tmuxp.git-pull.com/configuration/examples.html
```