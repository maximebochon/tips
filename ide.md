# Tips on IDEs (Integrated Development Environment)

## IntelliJ IDEA

Open a file in a new window: `CTRL`+`double-click`

Compare two files:
- select two files
- press `CTRL`+`D`

Find in path: `CTRL`+`MAJ`+`F`

Search everywhere: `SHIFT` `SHIFT`

## Vim

- `dd` : delete current line
- `dd`, `p` : move current line
- `yy`, `p` : duplicate current line
- `i` : switch to _insert_ mode (before cursor)
- `Esc` : exit _insert_ mode 
- `u` : undo
- `~` : toggle case
- `/pattern` : search for _pattern_
- `?pattern` : search backward for _pattern_
- `n` : repeat search in same direction
- `N` : repeat search in opposite direction
- `:%s/old/new/g` : replace all _old_ with _new_ throughout file
- `:%s/old/new/gc` : replace all _old_ with _new_ throughout file with confirmations
- `:w` : save
- `:q` : quit (fails if there are unsaved changes)
- `:q!` : quit and throw away unsaved changes
- `:wq` : save and quit
