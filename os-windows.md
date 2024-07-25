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
- enter the `TaskBar` directory, it should contain shortcuts to these applications
- there may also be an `ImplicitAppShortcuts` directory containing other shorcuts

&nbsp;

Display HTTP proxy settings:

```bat
netsh winhttp show proxy
```

&nbsp;

Set the window of an application always on top of others knowing its PID (Windows 7 and above):
- open a _PowerShell_ terminal (`WIN+R`, `powershell`, `⮠ `)
- replace the value of the target PID in this script and run it:

```powershell
$targetPID = 12345
$signature = @'
[DllImport("user32.dll")] public static extern bool SetWindowPos(
IntPtr hWnd, IntPtr hWndInsertAfter, int X, int Y, int cx, int cy, uint uFlags);
'@
$api = Add-Type -MemberDefinition $signature -Name NativeAPI -Namespace NativeAPI -Using System.Text -PassThru
$window = (Get-Process -id $targetPID).MainWindowHandle
$api::SetWindowPos($window, -1, 0, 0, 0, 0, 0x0003) # use -2 instead of -1 to cancel the 
```

- [this other script](https://github.com/bkfarnsworth/Always-On-Top-PS-Script/blob/master/Always_On_Top.ps1) does the same in a more advanced manner:
a GUI is shown to select the targeted window without having to know its PID

&nbsp;

Mount a directory as a drive:

```bat
subst D: C:\DATA
```

&nbsp;

Lock current session:
- from the keyboard: `WIN`+`L`
- from the command line: ```rundll32.exe user32.dll,LockWorkStation```

&nbsp;

Trigger `CTRL`+`ALT`+`END` from a _Remote Desktop_ session to get the same behaviour as `CTRL`+`ALT`+`DEL`.

&nbsp;

On a French AZERTY keyboard, use the `WIN`+`;` shortcut to acess the emoji pop-up window.

&nbsp;

Files containing system icons:
- `%SystemRoot%`
  - `explorer.exe`
  - `System32`
    - `ddores.dll`
    - `dsuiext.dll`
    - `ieframe.dll`
    - `imageres.dll`
    - `mstscax.dll`
    - `mstsc.exe`
    - `networkexplorer.dll`
    - `setupapi.dll`
    - `shell32.dll`
    - `wmploc.dll`
