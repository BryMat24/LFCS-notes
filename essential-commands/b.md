# 📑 Compare and Manipulate File Content

Essential Linux commands for LFCS exam practice.

---

## 🔍 Comparing Files

### diff

Compare line by line.

```bash
diff file1 file2
diff -y file1 file2
```

### uniq

```bash
uniq file.txt                  # Remove consecutive duplicate lines
uniq -c reading.txt            # Show occurrences of each line
uniq -u reading.txt            # Show only unique values
uniq -d reading.txt            # Show only duplicate values
```

### sorting

```
sort file.txt                  # Alphabetical sort
sort -r file.txt               # Reverse sort
sort -n numbers.txt            # Numeric sort
sort -k 2 file.txt             # Sort by 2nd column (default delimiter = space)
sort -t: -k 3 /etc/passwd      # Sort by 3rd field, using ":" as delimiter
```

### cut

```
cut -d ' ' -f 1 file           # Print first column (delimiter = space)
cut -d ' ' -f 1,3 file         # Print first and third columns
```

### Viewing File Sections

```
tail file.txt                  # Last 10 lines
tail -n 5 file.txt             # Last 5 lines
tail -f /var/log/syslog        # Follow file (useful for logs)

head file.txt                  # First 10 lines
head -n 2 file.txt             # First 2 lines
```

### Counting

```
wc /etc/passwd                 # Lines, words, bytes
wc -l /etc/passwd              # Just line count
wc -w /etc/passwd              # Just word count
wc -c /etc/passwd              # Just byte count
```

### Character Translation

```
tr 'a-z' 'A-Z' < file.txt      # Convert lowercase → uppercase
tr -d '0-9' < file.txt         # Remove digits
```
