# 📑 Advanced Permissions: SUID, SGID, and Sticky Bit

---

## 1. 🔹 Special Permission Values

Each advanced permission has a **numeric value**:

-   **SUID (Set User ID)** → `4`
    -   Executable runs as **file owner**.
-   **SGID (Set Group ID)** → `2`
    -   Executable runs as **file’s group**.
    -   On directories: new files inherit the directory’s group.
-   **Sticky Bit** → `1`
    -   On directories: files can only be deleted by the **file’s owner** (or root).

## 2. 🔢 Numeric Representation

Special bits go in **front** of normal file permissions:

Examples:

-   `chmod 4755 file` → SUID + rwxr-xr-x
-   `chmod 2755 file` → SGID + rwxr-xr-x
-   `chmod 1755 dir` → Sticky + rwxr-xr-x
-   `chmod 6755 file` → SUID + SGID + rwxr-xr-x
-   `chmod 7755 dir` → SUID + SGID + Sticky + rwxr-xr-x

## 3. 🔧 Symbolic Representation

You can also use symbolic flags:

-   `chmod u+s file` → add SUID
-   `chmod g+s file` → add SGID
-   `chmod +t dir` → add sticky bit

Remove with `-s` or `-t`.

## 4. 🔍 Verification

Check permissions with `ls -l`:

-   SUID → `s` in **user/owner execute** bit (`rwsr-xr-x`)
-   SGID → `s` in **group execute** bit (`rwxr-sr-x`)
-   Sticky bit → `t` in **others execute** bit (`drwxrwxrwt`)
