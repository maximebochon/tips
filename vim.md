# Vim

> Vi IMproved, a programmers text editor.

- `dd` : delete current line
- `yy`, `p` : duplicate current line
- `i` : switch to _insert_ mode (before cursor)
- `Esc` : exit _insert_ mode 
- `u` : undo
- `:w` : save
- `:q` : quit (fails if there are unsaved changes)
- `:q!` : quit and throw away unsaved changes
- `:wq` : save and quit
- `/pattern` : search for _pattern_
- `?pattern` : search backward for _pattern_
- `n` : repeat search in same direction
- `N` : repeat search in opposite direction
- `:%s/old/new/g` : replace all _old_ with _new_ throughout file
- `:%s/old/new/gc` : replace all _old_ with _new_ throughout file with confirmations
