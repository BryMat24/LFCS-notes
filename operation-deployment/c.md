## Logs

--
Modern distros (RHEL 7+/Ubuntu 16+) use systemd-journald as the main logging service. Can persist logs across reboots if /var/log/journal/ exists.

```
journalctl
journalctl -f # follow
journalctl -u sshd # logs for unit sshd
journalctl -b -1 # previous boot logs
journalctl --since "2 hours ago"
journalctl --since "2025-09-12 08:00:00" --until "2025-09-12 09:00:00"
journalctl -p err # priority
journalctl -p warning
journalctl -k
```
