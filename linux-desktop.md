# Linux Desktop tips

:bookmark: Remove unwanted default bookmarks in _Nautilus_:
- edit `~/.config/user-dirs.dirs`
- comment unwanted variables (`XDG_TEMPLATE_DIR`, `XDG_PUBLICSHARE_DIR`...)
- edit `/etc/xdg/user-dirs.defaults`
- comment unwanted variables (`TEMPLATES`, `PUBLICSHARE`...)
- launch _Nautilus_
- remove remaining unwanted bookmarks via the right-click _remove_ command
