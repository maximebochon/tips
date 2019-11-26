# Windows tips

:clock2: Display Windows start-up date and time:
- open a _PowerShell_ terminal (`WIN+R`, `powershell`, `⮠ `)
- type the following command: `(gcim Win32_OperatingSystem).LastBootUpTime`

&nbsp;

:arrow_forward: Launch programs at start-up (Windows 7 and above):
- open the start-up directory by running (`WIN+R`):
  - `shell:startup` for personal use
  - `shell:common startup` for common use
- put shortcuts you want to launch at start-up in that directory

&nbsp;

Get the shortcut of an application pinned in the taskbar (Windows 7 and above):
- type `WIN+R` and run `shell:user pinned`
- enter the `TaskBar` directory
- it should contain shortcuts to these applications

&nbsp;

Display HTTP proxy settings:
```bat
netsh winhttp show proxy
```
