# Diagnose & Manage Process

---

### ps (process snapshot)

```
ps aux            # all processes, full details
ps -ef            # alternative full listing
ps -u bob         # processes owned by user bob
```

pid - process ID of the process

It is set when process start, this means that provide info on starting order of processes
%cpu - It is the CPU time used divided by the time the process has been running.

%mem - ratio of the process’s resident set size to the physical memory on the machine

VSZ (virtual memory) - virtual memory usage of entire process (in KiB)

RSS (resident memory) - resident set size, the non-swapped physical memory that a task has used (in KiB)

tty - On which process is running.

NOTE: ? means that isn't connect to a tty
stat - process state

start- starting time or date of the process

time - cumulative CPU time

command - command with all its arguments

In /proc/[pid]

There is a numerical subdirectory for each running process; the subdirectory is named by the process ID.

/proc/[pid]/fd

This is a subdirectory containing one entry for each file which the process has open, named by its file descriptor, and which is a symbolic link to the actual file. Thus, 0 is standard input, 1 standard output, 2 standard error, and so on.

### top (real-time monitoring)

```
top
```

Keys:

M → sort by memory

P → sort by CPU

k → kill process

q → quit

### Finding Processes

```
pgrep sshd
pgrep -u bob
```

### Process States

Check STAT column in ps:

-   R → Running

-   S → Sleeping (idle)

-   D → Uninterruptible sleep (usually I/O wait)

-   T → Stopped (e.g., Ctrl+Z)

-   Z → Zombie (process finished but parent didn’t clean up)

### Managing Process

```
kill pid
```

Send a SIGTERM to process with pid equal to pid, allows for cleanup

```
kill -9 pid
```

Send a SIGKILL to process with pid equal to pid

```
kill -number pid
```

Send a signal that correspond to number to process with pid equal to pid

```
kill -l
```

List all available signal and corresponding number

### Process Priority

```
nice -n value command &
```

```
renice -n value pid
```

### Foreground / Background Jobs

```
command &
fg %1
bg %1
jobs
```

### Open files

```
lsof -u bob # which files this user opens
lsof -p 1234 # which files this process opens
lsof /var/log/syslog # which process is opening this file
lsof -i :22 # which port is opening this port
```

### Cron

### 1. User vs System Cron

-   **System-wide cron**:  
    `/etc/crontab`

-   **Cron directories**:
-   `/etc/cron.d/`
-   `/etc/cron.daily/`
-   `/etc/cron.hourly/`
-   `/etc/cron.weekly/`
-   `/etc/cron.monthly/`

### 2. Crontab

| Field        | Values                               |
| ------------ | ------------------------------------ |
| Minute       | 0–59                                 |
| Hour         | 0–23                                 |
| Day of Month | 1–31                                 |
| Month        | 1–12 (or names: Jan, Feb, …)         |
| Day of Week  | 0–7 (0 & 7 = Sunday, Mon=1, … Sat=6) |

### Special characters:

-   `*` → any value
-   `,` → list (e.g., `1,15`)
-   `-` → range (e.g., `1-5`)
-   `/` → step (e.g., `*/10` = every 10 units)

### 3. Managing Crontabs

-   Edit current user’s crontab:
    ```bash
    crontab -e
    crontab -l
    crontab -r
    crontab -u bob -e
    ```

### Anacron

Only has system-wide, located at /etc/anacrontab

```
# period   delay   job-identifier   command
1   5   cron.daily   run-parts /etc/cron.daily
7   10  cron.weekly  run-parts /etc/cron.weekly
30  15  cron.monthly run-parts /etc/cron.monthly
```

Can only run daily/weekly/monthly

```
sudo anacron -f -n # reset
```

### At

at lets you schedule a one-time job to run at a specific time in the future.

Submit a job:

```
at 22:00
```

(then type commands, end with Ctrl+D)

List jobs:

```
atq
```

Remove job:

```
atrm <jobid>
```

View job details:

```
at -c <jobid>
```

## Resource Management

---

```
free -h
du -sh file.txt
df -h
uptime
lscpu
fsck /dev/vdb # for ext
xfs_repair /dev/vdb
```
