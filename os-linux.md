# Linux tips

:label: Get general OS and distribution information:
- `lsb_release -a`
- `hostnamectl`
- `cat /etc/issue`
- `cat /etc/*-release`
- `cat /etc/*-version`

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

:high_brightness: Adjust laptop backlight brightness the hard way:
```bash
cd /sys/class/backlight/acpi_video0
sudo su root
echo $BRIGHTNESS > brightness
# with $BRIGHTNESS from 0 to ./max_brightness
exit
```

&nbsp;

:lizard: Show process information by clicking on a window:
```bash
ps -p $(xprop | awk '/PID/ {print $3}') -o user,pid,args
```

&nbsp;

:minidisc: Monitor per process input/output usage:
```bash
sudo iotop
# show every process, refresh every second

sudo iotop --only --delay=5
# show only processes with I/O activity, refresh every 5 seconds
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

&nbsp;

:ping_pong: Set a proxy configuration for [APT](https://en.wikipedia.org/wiki/APT_%28software%29):
- Add the adapted following lines to `/etc/apt/apt.conf.d/proxy.conf`:
```sh
Acquire::http::Proxy "http://username:password@proxy-ip:proxy-port/";
Acquire::https::Proxy "https://username:password@proxy-ip:proxy-port/";
```
- In some cases, it may look simpler (no authentification, same for HTTP and HTTPS, no S for HTTPS):
```sh
Acquire::http::Proxy "http://10.31.255.65:8080/";
Acquire::https::Proxy "http://10.31.255.65:8080/";
```

&nbsp;

:watch: Display, in real time, detailed system date and time information:
```sh
watch --interval 1 timedatectl
```
```
                Local time: sam. 2024-05-04 15:26:01 CEST
            Universal time: sam. 2024-05-04 13:26:01 UTC
                  RTC time: sam. 2024-05-04 13:26:00
                 Time zone: Europe/Paris (CEST, +0200)
 System clock synchronized: no
               NTP service: inactive
           RTC in local TZ: no
```

## Free some space

### Journals

```sh
sudo journalctl --vacuum-size=100M
# Keep only most recent 100M of data.
```

### APT

```sh
sudo apt autoremove
sudo apt autoclean
sudo apt clean
```
