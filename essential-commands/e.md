# 📑 Soft Links vs Hard Links in Linux

---

## 🔹 What is a Link?

A **link** is a pointer to a file.  
Linux has two types of links:

-   **Hard link**
-   **Soft (symbolic) link**

## 1. 🔗 Hard Links

-   A hard link is another **name for the same inode** (the same file on disk).
-   Multiple filenames can point to the **same data blocks**.
-   Deleting one hard link **does not delete the data** until all hard links are removed.

### Example

```bash
# Create a hard link
ln file.txt hardlink.txt

# Verify (same inode number)
ls -li
```

## 2. Soft Links

-   A soft link is like a shortcut to another file.
-   It stores a pathname pointing to the target.
-   If the original file is deleted, the symlink becomes dangling (broken).

```
# Create a soft link
ln -s file.txt softlink.txt

# Verify (shows arrow ->)
ls -l
```
