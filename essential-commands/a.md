# FIND Command in Linux

`find <path> [option] [expression]`

---

## 🔍 Basic Examples

```bash
# Search in /etc for files containing "host" in their name
find /etc -name "*host*"

# Find files with permission 777 and remove them
find /home/user -perm 777 -exec rm '{}' +
```

## Exact Value Parameters

Some parameters accept a numeric value n with + or -:

-   +n → greater than n
-   -n → less than n
-   n → exactly n

```
find . -maxdepth 3 -type f -size +2M
```

## Logical Operators

```
# OR condition (files named name1 OR name2)
find . \( -name name1 -o -name name2 \)

# NOT condition (exclude files owned by 'owner')
find . \! -user owner
```

## Case Sensitive

```
# Search for files ignoring case
find . -iname name
```

## Permission Related

```
# Files with permissions exactly 222
find . -perm 222

# Files with at least permissions 222 (e.g. 777 will match)
find . -perm -222

# Files with write permission for owner OR group OR others
find . -perm /222

# Files with at least write permission for group
find . -perm -g=w
```

## Time based

```
# Files accessed at least 2 days ago (more than 24 hours)
find . -atime +1
```

## 📌 Quick Notes

-type f → file

-type d → directory

-delete → directly delete matching files

-exec <cmd> {} \; → execute command per file (slower)

-exec <cmd> {} + → execute command in batches (faster)
