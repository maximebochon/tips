# Virtual Box

In the context of a Windows host and Linux guests.

## Convert fixed size VMDK disk image to dynamic size VDI

```
VBoxManage.exe clonemedium vm-disk.vmdk vm-disk.vdi --format VDI --variant Standard
```

## Shrink size of dynamic size VDI disk image

1. From the Linux VM, install `zerofree` utility:

```sh
sudo apt install zerofree
```

2. From the Linux VM recovery mode, open a root prompt and prepare empty space to compacting:

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

3. From a Windows command terminal, run the Virtual Box compacting command:

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
