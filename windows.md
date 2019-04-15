# Windows tips

:clock2: Display Windows start-up date and time (among other information):
```bat
net statistics workstation
```
(i.e. date and time at which the Windows login prompt appeared to the user)

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
