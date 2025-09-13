# 📑 Analyze Text with Regular Expressions

---

## 🔹 File Globbing

Globbing = pathname expansion handled by the **shell** before executing the command.

### Patterns

1. `*` → Matches **0 or more characters**
2. `?` → Matches **exactly 1 character**
3. `[...]` → Matches **any one character from the class**
4. `{...}` → **Brace expansion** (generates string lists)
5. `\` → **Escape glob** so it’s treated literally
6. `**` → Matches files/dirs recursively (with `shopt -s globstar`)

---

### Common Commands Using Globbing

#### 1. File Management

```bash
ls *.txt                  # list all .txt files
cp *.jpg /backup/         # copy jpg files
mv report??.txt /tmp/     # move files like report01.txt, reportAB.txt
rm file[1-3].log          # remove file1.log, file2.log, file3.log
```

#### 2. Text Processing

```
cat *.conf                # concatenate all config files
grep "ERROR" logs/*.log   # search all log files
wc -l *.sh                # count lines in all shell scripts
```

#### 3. Archiving / Compression

```
tar -czf archive.tar.gz *.txt   # compress all text files
zip images.zip *.png            # zip all png files
```

## 📑 Grep Patterns (Regex)

Use:

```bash
grep -E <pattern> <path>
```

| Character  | Definition                           | Example          | Matches                       |     |          |
| ---------- | ------------------------------------ | ---------------- | ----------------------------- | --- | -------- |
| `^`        | Start of string                      | `^abc`           | `abc`, `abcd`, `abc1`         |     |          |
| `$`        | End of string                        | `abc$`           | `abc`, `rasabc`, `2aabc`      |     |          |
| `.`        | Any character (except newline)       | `a.c`            | `abc`, `acc`, `a1c`           |     |          |
| `\|` or \` | \`                                   | Alternation (OR) | `a\|b` / \`a                  | b\` | `a`, `b` |
| `{n}`      | Explicit quantity of preceding char  | `ab{2}c`         | `abbc`                        |     |          |
| `[...]`    | Explicit set of characters           | `a[bB]c`         | `abc`, `aBc`                  |     |          |
| `[a-z0-9]` | Range (lowercase letters or numbers) | `a[a-z0-9]c`     | `aac`, `a1c`                  |     |          |
| `( ... )`  | Group of characters                  | `(abc){2}`       | `abcabc`                      |     |          |
| `*`        | Zero or more of preceding char       | `a*bc`           | `bc`, `abc`, `aabc`, `aaaabc` |     |          |
| `+`        | One or more of preceding char        | `a+bc`           | `abc`, `aabc`                 |     |          |
| `?`        | Zero or one of preceding char        | `a?bc`           | `bc`, `abc`                   |     |          |
| `^$`       | Empty string (matches blank line)    | —                | Matches empty line            |     |          |

## 📑 Essential `sed` Commands

`sed [options] 'command' file`

⚠️ Without the `-i` option, the results are shown only on **standard output** and the file itself is **not modified**.

---

## 1. 🔄 Substitute (Search & Replace)

```bash
# Replace first occurrence of "error" with "issue" in each line
sed 's/error/issue/' file.txt

# Replace all occurrences
sed 's/error/issue/g' file.txt

# Replace all occurrences (case-insensitive)
sed 's/error/issue/gI' file.txt

# Replace only the second occurrence in each line
sed 's/error/issue/2' file.txt

# Replace on the 10th line only
sed '10s/error/issue/' file.txt
```

## 2. ❌ Delete Lines

```
sed '2d' file.txt           # Delete line 2
sed '2,5d' file.txt         # Delete lines 2–5
sed '/debug/d' file.txt     # Delete lines containing "debug"
```

## 3. 📑 Extract (Print Only)

```
sed -n '5p' file.txt        # Print line 5
sed -n '5,10p' file.txt     # Print lines 5–10
sed -n '/ERROR/p' file.txt  # Print lines containing "ERROR"
```

## 4. ➕ Insert & Append

```
sed '3i This is inserted' file.txt   # Insert before line 3
sed '3a This is appended' file.txt   # Append after line 3
```
