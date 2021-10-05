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
