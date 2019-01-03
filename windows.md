# Windows tips

:clock2: Display Windows start-up date and time (among other information):
```bat
net statistics workstation
```
(i.e. date and time at which the Windows login prompt appeared to the user)

&nbsp;

:arrow_forward: Launch programs at start-up :
- open the start-up directory by running (`WIN+R`) :
  - `shell:startup` for personal use
  - `shell:common startup` for common use
- put shortcuts you want to launch at start-up in that directory
