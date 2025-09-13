# 📑 Archive, Backup, Compress, Unpack, and Uncompress Files

---

## 🔹 General Syntax

```bash
tar [options] archive.tar files...
```

1. Create Archives

```
tar -cf archive.tar file1 file2 dir/
```

-   -c → create new archive
-   -f → specify filename (archive.tar)

2. Extract Archives

```
tar -xf archive.tar
tar -xf archive.tar -C /tmp/extract_here # extract to specific directory
tar -tf archive.tar # list files in archive
```

-   -x → extract files
-   -f → specify archive filename

3. Compression

```
# gzip
tar -czf archive.tar.gz file1 dir/
tar -xzf archive.tar.gz

# bzip2
tar -cjf archive.tar.bz2 file1 dir/
tar -xjf archive.tar.bz2

# xz
tar -cJf archive.tar.xz file1 dir/
tar -xJf archive.tar.xz
```

4. Update Archives

```
tar -rf archive.tar newfile.txt   # Append new file(s) to archive
tar -uf archive.tar file.txt      # Update file if newer than archived copy
```

## Backup a device

Using dd

```
dd if=/dev/sda of=/backup/sda.img bs=64K conv=noerror,sync status=progress
```

-   if=/dev/sda → input file (device to back up)

-   of=/backup/sda.img → output file (backup image)

-   bs=64K → block size (bigger = faster)

-   conv=noerror,sync → continue on errors, pad blocks if needed

-   status=progress → show progress

## Using rsync (File-Level Backup)

rsync is preferred for incremental backups (only changes are copied).

Basic Copy

```
rsync -av /home/ /backup/home/
```

-   -a → archive mode (preserves permissions, timestamps, symlinks)

-   -v → verbose

-   /home/ → note the trailing /, means "contents of /home"

Sync Between Hosts (via SSH)

```
rsync -avz /home/ user@remote:/backup/home/
```

-z means that content will be compressed during transfer
