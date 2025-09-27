# Remote Filesystem

---

## NFS

Server

```
sudo apt install nfs-kernel-server

sudo vim /etc/exports
# /srv/homes    hostname1(rw, sync, no_subtree_check)   hostname2(rw, sync, no_subtree_check)
# hostname = can be IP or subnet or wildcardP
# sync / async = ensure data written by client is actually stored in storage device before reported or not

man exports
sudo exportsfs -r   # refresh what is shared, from the /etc/exports
```

Client

```
sudo apt install nfs-common
sudo mount IP_hostname_server:/path/to/remote/dir /path/to/local/dir

sudo vim /etc/fstab
# IP_server:/etc /mnt nfs defaults 0 0
```

## NBD

The server exposes block devices, the client are able to manage the filesystem themselves

Server

```
sudo install nbd-server

sudo vim /etc/nbd-server/config

sudo systemctl restart nbd-server.service

man 5 nbd-server
```

etc/nbd-server/config

```
[generic]
    # user =
    # group =
    includedir = /etc/nbd-server/conf.d
    allowlist = true # allow client to list what block devices are present

[partition2]
    exportname=/dev/sda1
```

Client

```
sudo apt install nbd-client

sudo modprobe nbd # load kernel module temporarily

sudo vim /etc/modules-load.d/module.conf # put nbd here

sudo nbd-client <IP> -N <PARTITION>

sudo mount /dev/nbd0 /mnt

sudo umount /dev/nbd0 /mnt

sudo vim /etc/fstab

sudo nbd-client -l <IP>
```
