tmux Cheatsheet

# Starting

* `$ tmux`
* `$ tmux new-session -s basic` Create a session named basic
* `$ tmux new -s basic` Create a session named basic

# Sessions

* `__PREFIX__ d` detach from our tmux session
* `$ tmux list-sessions` or `tmux ls` List sessions
* `$ tmux attach` Attach to our session
* `$ tmux new -s second_session -d` Create a new session and detach it immediately
* `$ tmux attach -d second_session` Attach to named session
* `$ tmux kill-session -t basic` Kill session named basic
* `$ tmux new -s windows -n shell` Create a session name "windows" and name the first window "shell"
* `__PREFIX__ s` Select sessions. Use the right arrow to select specific windows
* `__PREFIX__ (` Switch to previous session
* `__PREFIX__ )` Switch to next session
* `__PREFIX__ $` Rename session

# Windows

* `__PREFIX__ c` Create a new window
* `__PREFIX__ ,` Rename window
* `__PREFIX__ n` Next window
* `__PREFIX__ p` Previous Window
* `__PREFIX__ 4` Go to window 4 (starting from 0)
* `__PREFIX__ f` Find window by name
* `__PREFIX__ w` Display a visual menu of window

# Panes

* `__PREFIX__ %` Split window vertically
* `__PREFIX__ "` Split window horizontally
* `__PREFIX__ o` Cycle through panes
* `__PREFIX__ UP, DOWN, LEFT, RIGHT` Move around the panes
* `__PREFIX__ Cntrl-UP/DOWN/LEFT/RIGHT` Resize pane. Repeatable
* `__PREFIX__ SPACE` Cycle through default layouts
* `__PREFIX__ x` Kill pane - useful if you can't communicate with the process.

# Command Mode

* `__PREFIX__ :` Go into command mode
* `new-window -n processes "top"` Create a new window named `processes` running `top`

# Custom setups

* `tmux attach -t development` Attach to session named `development`
* `tmux split-window -v -t development` Split window in session named `development`
* `tmux new -s development -n machineOne -d` Create session named `development`, name window `machineOne` and detach immediately
* `tmux send-keys -t development 'cd CocoaApps' C-m`
* `tmux split-window -v -t development`
* `tmux  select-layout -t devlopment main-horizontal`
* `tmux send-keys -t development:0.1 'emacs' C-m` Open emacs in session `devlopment`, screen 0, window 1
* `tmux select-window -t development:1`

# Working with text

* `__PREFIX__ [` to enter copy mode, `ESC` to exit. Emacs bindings to select and copy. Vi mode also possible.

# Workflow

* `__PREFIX__ z` toggle pane zoom
* `: pipe-pane -o "log.txt"` Toggle output piping to log.txt
* `: pipe-pane -o "cat >> ~/#W.log" \; display "Toggled logging to ~/#W.log"` Toggle output piping to log.txt
