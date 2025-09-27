## Storage Monitoring

---

Stress on device either through too frequent writes/reads, or high volume of data is read / written at once:

-   tps = transfer per second
-   KB_read/s
-   KB_write/s

```
sudo apt install systat # install iostat
sudo iostat # show read since the start of the boot
iostat 1 # iostat refresh every 1 second, now iostat doesn't show average usage since booted, but in the last 1 second

pidstat -d # how processes are using our storage devices
pidstat -d 1 # refresh every 1s
```

```
sudo dmsetup info /dev/dm-0 # see mapping lvm to actual device
```
