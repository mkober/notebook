* Start TMUX if not already running in .bashrc
tmux attach -t dev || tmux new -s dev
export TMUX_INACTIVE="true"

* Enable mouse support and terminal scroll
set -g mouse on
set -g history-limit 10000
set -g mode-mouse on
