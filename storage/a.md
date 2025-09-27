# Storage Management

---

### Managing Partition

```
lsblk - see block devices in our computer
```

List partition on this block device: sda

```
fdisk --list /dev/sda
cfdisk /dev/sda # Creating partition from this device
```

### Manage Swap

See if our system use any swaps

```
swapon --show
```

configuring swaps using partition

```
sudo mkswap /dev/vdb3 # format this partition as swap
sudo swapon --verbose /dev/vdb3 # temporary
sudo swapon --show
sudo swapoff /dev/vdb3
```

configuring swaps using file

```
sudo dd if=/dev/zero of=/swap bs=1M count=128 status=progress
sudo chmod 600 /swap
sudo mkswap /swap
sudo swapon --verbose /swap
```

### Filesystems

```
sudo mount /dev/sdb /mnt
sudo umount /dev/sdb /mnt
```

-   xfs = red hat
-   ext4 = ubuntu

```
# Simplist way to make file system on partition.
mkfs.xfs /dev/sdb1, mkfs.ext4 /dev/sdb1
mkfs.xfs -i size-512 -L “BackUpVolume” /dev/sdb1

mkfs.ext4 /dev/sda1
```

editing filesystem properties

```
xfs_admin -L "<label>" /dev/sda1
tune2fs -L "<label>" /dev/sda1
```

/etc/fstab - onboot up

reload by systemctl daemon-reload

```
blockdev, /mountpoint filesystem(xfs) default(mount options) 0(dump) 0,1,2(scan for errors), 0 for swap, 1 for root and 2 for others
```

blkid /dev/sda1 = SHow UUID of device and other filesystem properties

### Filesystems Options

findmnt - finds everything mounted.

```
findmnt -t xfs,ext4
mount -o ro,noexec,nosuid /dev/vdb2 /mnt
```

-   noexec = can’t run a program
-   nosuid - disable suid so root program can’t run with sudo

Only mount once, but can remount - only for not specific file system usage, use umount then

mount -o remount,rw,noexec,nosuid /dev/vdb2 /mnt

Mount options apply to all filesystems: man mount

some to filesystem: man xfs - has a mount option section
mount -o allocsize=32k /dev/vdb1 /mybackups
mount -a :mount all in fstab
