qHere are some tools to write code and run [[CLI]] commands in a [[Linux]] system. 
# TMUX
- `Ctrl + b %` : Split the terminal horizontally;
- `Ctrl + b "`: Split the terminal vertically;
- `Ctrl + b o` : Navigate to another panel;
- `Ctrl + b [` : Enable Scroll mode (`q` to quit);
- `Ctrl + b arrow` : Navigate to arrow direction panel;
- `Ctrl + b + arrow` : Resize in arrow direction;
- `Ctrl+b d` : Remove a panel;
- `tmux ls`: List the active sections;
- `tmux attach-session -t 0`: Attach to exist session;
- `tmux attach-session -t 0`: Delete a session;
___
# Tilix
##### Terminals:
- `Ctrl + Alt + r` : Split the terminal horizontally;
- `Ctrl + Alt + d`: Split the terminal vertically;
- `Ctrl + Shift + w`: close current terminal
- `Shift + Alt + Arrows`: Resize the terminal in the direction o arrow;
- `Alt + Arrows`: Navigate to terminal in the direction o arrow;
##### Sessions:
- `Ctrl + Shift + t` : Create new session;
- `Ctrl + Shift + q`: Remove current serrion;
- `Ctrl + PageUp`: Jump to previous session;
- `Ctrl + PageDown`: Jump to next serrion;

---

# Vim
Pressing `i` or `a`, that means insert and append respectively, you can change from the command mode to editing mode. To return to command mode, you should press `esc`.
#### Saving
In the command mode, something can be saved using `:w /tmp/test.cs`, where it means that I am writing some new content or modifications in the test.cs file. If a existent file is open, you can simply use `:w`, that write content in the current file. The command `:w!` can also be used, in the case where need to force the write, it'll overwrite an existing file without asking for confirmation.
#### Quit
`:q` allows you to quit from a file. That can be combined with the `:w` to write and quit the editor.
### Navigating
In the command mode, the `h`, `j`, `k` and `l` can be user as arrows to navigate in the content, where h is left, l is right, k is up and j is down. It is possible combine those with numbers to repeat some times automatically, for example `10k` navigates up ten lines  
`gg` navigate to the top(first line) of content and `G` to the end(last line).

## Navigating:
- `w`: Word by word;
- `b`: Backward word by word;
- `e`: Word by word, to the end of word;
- `0 and $`: To start and end of line;
- `gg and G`: First and last line of file;
- `f + char`: To to the next char;
- `F + char`: To to the previous char;
## LunarVIim
- `Ctrl+h` : Navigate to file tree (left);
- `Ctrl+l`: Navigate to text editor (right);
- `:Lazy`: Show all plugins; (`gb` to load plugins)
## GVim
- `Ctrl+w s` : Split the terminal horizontally;
- `Ctrl+w v`: Split the terminal vertically;
- `Ctrl+w c`: Close a panel;
- `Ctrl+w {h, j, k and l}`: To navigate the panels;