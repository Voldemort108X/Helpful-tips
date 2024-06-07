# Motivation
Let your cmd terminal run in the backend.

1. Create a screen/session
```
tmux new -s session_name
```
2. Detach from a session: ctrl+b and then type the word: d
3. List the tmux sessions
```
tmux ls
```
4. Attach the session:
```
tmux a -t session_name
```
5. Kill the session:
```
tmux kill-session -t session_name
```
