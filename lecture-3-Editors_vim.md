# Lecture 3 - Editors (vim)
[Lecture notes](https://missing.csail.mit.edu/2020/editors/)

**Vim** is a modal editor, it has different modes for viewing, inserting and editing text. The purpose of key combination change between the modes and there are also key combinations to switch between modes.

Vim starts up in *normal* mode. Hitting `i` will switch to *insert* mode. Hitting `esc` will switch back to *normal* mode. There is also a *replace* mode which overwrittes existing text, which can be entered by hitting `r` key. 

`:` is used to enter the *command* mode.

`:q` closes the current window. Where there are unsaved changes, either use `wq` to save (write) and quit or `q!` to discard unsaved changes.

When there are multiple windows, use `qa` to quit all windows and exit vim. 

`H`, `J`, `K` and `L` can be used to move left, down, up and right respectively in normal mode.
