## Managing LVM

---

**Concepts**:

-   Physical Volumes (PV): Actual storage device, hard disk partition
-   Volume Group (VG): A pool of storage created by combining one or more physical volumes.
-   Logical Volume (LV): A virtual partition, created inside a volume group, mountable like normal partitions
-   Physical Extent (PE): Smallest chunk of storage in LVM. Logical Volumes are made up of extents from volume group

```
sudo apt update
sudo apt install lvm2 -y

sudo lvmdiskscan # see what PVs we can use

sudo pvcreate /dev/sdc /dev/sdd # create physical volumes to LVM

sudo pvs # see physical devices here

sudo vgcreate my_volume /dev/sdc /dev/sdd # vgcreate [name_of_group] [name_of_pv]

sudo vgextend my_volume /dev/sde

sudo vgreduce my_volume /dev/sde

sudo pvremove /dev/sde # remove physical volume
```

create logical volume

```
sudo lvcreate --size 2G --name partition1 my_volume

sudo lvresize --extents 100%VG my_volume/partititon1 # use remaining

sudo lvresize --size 3G my_volume/partition1 # but doesn't resize filesystem
```

create partition

```
# dev/name_of_volume_group/name_of_logical_volume -> path to LV

sudo mkfs.ext4 /dev/my_volume/partition1

sudo lvresize --resizefs --size 3G my_volume/partition1
```
