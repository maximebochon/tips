# VirtualBox notes

In the context of a _Windows_ host and _Linux_ guests.

## Convert fixed size VMDK disk image to dynamic size VDI

From a _Windows_ command terminal, run the _VirtualBox_ clone command with options:

```
VBoxManage.exe clonemedium vm-disk.vmdk vm-disk.vdi --format VDI --variant Standard
```

## Shrink size of dynamic size VDI disk image

1. From the _Linux_ VM, install `zerofree` utility:

```sh
sudo apt install zerofree
```

2. From the _Linux_ VM recovery mode, open a root prompt and prepare empty space to compacting:

```sh
# Determine the device to work on and the type of file system used
df -Th

# Let say that (to be adapted):
DEVICE=/dev/sda1
FSTYPE=ext4

# Stop services that could be writing on the disk
systemctl stop systemd-journald.socket
systemctl stop systemd-journald.service
sudo swapoff -a

# Remount the device in read-only mode
mount -n -o remount,ro -t $FSTYPE $DEVICE /

# Prepare empty space for compacting
zerofree -v /dev/sda1

# Shut down the VM
shutdown -P now
```

3. From a _Windows_ command terminal, run the _VirtualBox_ compacting command:

```
VBoxManage.exe modifymedium disk vm-disk.vdi --compact
```

## Rename a virtual machine

From the GUI:
- select the virtual machine in the list
- open the _Settings..._ window
- under the _Basic_ tab of the _General_ section, use the _Name_ field to set a new name
- click the _OK_ button to apply the change

## Move a virtual machine

From the GUI:
- select the virtual machine in the list
- open the _Move..._ window
- select the desired parent directory for the directory containing the virtual machine
- click the _Select_ button to apply the change

## Rename/move a virtual disk

From the GUI:
- open the _Virtual Media Manager..._ window from the _File_ menu (or `CTRL`+`D`)
- select the virtual disk in the list
- under the _Attributes_ tab, use the _Location_ field to set a new name and/or location
- click the _Apply_ button to apply the change(s)

## Transfer files between host and guest without mounting a shared folder

From a running virtual machine window:
- open the _File Manager..._ window from the _Machine_ menu
- enable all panels (_Session_, _Options_, _Operations_, _Log_)
- type a valid user name and password in the dedicated fields
- click the _Create Session_ button to connect to the virtual machine
- use the left (host) and right (guest) file explorers to transfer files between host and guest systems
- click the _Close Session_ button when done

## Automatically mount a Windows host folder in the Linux guest VM

These are the requirements for a Linux VM user to be able to access automatically mounted shared folders:
- the _Guest Additions_ must have been installed properly in the VM
- the user in the VM must belong to the group `vboxsf`: `sudo adduser $USER vboxsf`

Provided the requirements are fulfilled:
- user the _Devices_ > _Shared Folders_ > _Shared Folder Settings..._ window to define a new shared folder
- choose a name to identify the shared folder from inside the Linux guest VM
- check options _Auto-mount_ and _Make Permanent_
- leave the field _Mount point_ empty
- save and validate (_OK_ button twice)

A new _media_ should be detected and automatically mounted in the Linux guest, here: `/media/sf_<name>/`

## Higher screen resolution at startup

_This information is unsure and should be treated cautiously._

It seems that from version 6.1 of VirtualBox, the screen resolution at startup is fixed to 800×600 pixels which is quite low for some modern graphical Linux installers.

A workaround to that is to check the _Enable EFI (special OSes only)_ option in the _Motherboard_ tab of the _System_ settings **before installing Linux**.

Be carefull: switching _EFI_ on after having already installed Linux may lead to major malfunction of the VM.
