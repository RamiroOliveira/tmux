# tmux
Tmux configuration file

My .tmux.conf file 

## Instalation
```
cd ~
git clone http://github.com/RamiroOliveira/tmux.git ~/.tmux
ln -s ~/.tmux/tmux.conf ~/.tmux.conf
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
tmux source ~/.tmux.conf
ctrl-c + I
```

## .bashrc
Add this to .bashrc

```
auto_tmux() {
  # Skip if already inside tmux
  [ -n "$TMUX" ] && return

  # Determine session type
  if [ -n "$SSH_CONNECTION" ]; then
    session="tmux-ssh"
  elif [ -n "$DISPLAY" ] || [ -n "$WAYLAND_DISPLAY" ]; then
    session="tmux-gui"
  else
    # Fallback if session type is unclear
    session="tmux-unknown"
  fi

  # Attach or create session
  if tmux has-session -t "$session" 2>/dev/null; then
    exec tmux attach-session -t "$session"
  else
    exec tmux new-session -s "$session"
  fi
}

auto_tmux
```
