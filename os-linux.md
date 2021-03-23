# Linux tips

Get general OS and distribution information:
- `lsb_release -a`
- `hostnamectl`
- `cat /etc/issue`
- `cat /etc/os-release`

&nbsp;

:bookmark: Remove unwanted default bookmarks in _Nautilus_:
- edit `~/.config/user-dirs.dirs`
- comment unwanted variables (`XDG_TEMPLATE_DIR`, `XDG_PUBLICSHARE_DIR`...)
- edit `/etc/xdg/user-dirs.defaults`
- comment unwanted variables (`TEMPLATES`, `PUBLICSHARE`...)
- launch _Nautilus_
- remove remaining unwanted bookmarks via the right-click _remove_ command

&nbsp;

:x: List invalid menu entries linking to non-existant programs (thanks to [ændrük](https://askubuntu.com/users/1859/ændrük) on [StackExchange](https://askubuntu.com/questions/40884/how-can-i-remove-orphaned-start-menu-entries)): 
```bash
for i in {/usr,~/.local}/share/applications/*.desktop; do
    which $(grep -Poh '(?<=Exec=).*?( |$)' $i) > /dev/null || echo $i;
done
```

&nbsp;

:whale: List largest installed packages:
```bash
# sudo apt install wajig
wajig large
```

&nbsp;

:lizard: Show process information by clicking on a window:
```bash
ps -p $(xprop | awk '/PID/ {print $3}') -o user,pid,args
```
&nbsp;

:tropical_drink: Verify and use a remote Samba storage:
- Check Samba availability and the share name to be used: `smbclient -N -L ${ip_address}`
```
# If not available you get:
Connection to ${ip_address} failed
```
```
# If available you get:
Sharename       Type   Comment
---------       ----   -------
${share_name}   Disk   ...
...
```
- Open the shared storage in _Thunar_: `thunar smb://${ip_address}/${share_name}/`
