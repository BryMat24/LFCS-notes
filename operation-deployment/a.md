# Boot, reboot, and shut down a system safely

---

### Power States

```
shutdown -h now shutdown
sudo reboot
```

### Boot or change system into different operating modes

1. BIOS -> do POST test, power on self test, test hardward, find disk and loads the bootloader
2. Boot loader -> bootloader loads the kernel
3. Kernel -> initializes system (RAM, CPU, etc), mounts root FS, launches init process
4. Init -> manages other processes

### Systemd

-   Currently used init process, defined by targets. Each target has their own dependencies that need to be met. Target files are found by .target file, they group together systemd units.
-   Systemd units are objects that systemd knows how to manage.

Targets

-   poweroff.target - shutdown system
-   rescue.target - single-user mode
-   multi-user.target - multi-user with networking
-   graphical.target - multi-user with networking and GUI
-   reboot.target - restart

```
systemctl get-default
```

It shows default target

```
systemctl list-units --type target --all
```

It shows all available targets

```
systemctl set-default multi-user.target
```

Set multi-user target as default

### Managing Service

```
systemctl daemon-reload      # applies new config
systemctl status sshd        # check service status
systemctl start sshd         # start service now
systemctl stop sshd          # stop service
systemctl restart sshd       # restart service
systemctl reload sshd        # reload config without stopping
systemctl enable sshd        # enable at boot
systemctl disable sshd       # disable at boot
systemctl is-enabled sshd    # check if enabled
systemctl is-active sshd     # check if running
```

### Unit files

Located in /usr/lib/systemd/system/ (default) and /etc/systemd/system/ (custom overrides).
service -> manage daemons

```
[Unit]
DescriptionOpenSSH server daemon
After=network.target

[Service]
ExecStart=/usr/sbin/sshd -D
ExecReload=/bin/kill -HUP $MAINPID
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

[Unit] = Metadata and dependencies

-   Description → human-readable text
-   Documentation → reference docs
-   Requires → hard dependency (must be active)
-   Wants → soft dependency
-   Before / After → ordering relative to other units

[Service] = Defines how services run

-   ExecStart= → main command to start the service
-   ExecReload= → command to reload the service configuration
-   ExecStop= → command to stop the service
-   Restart= → restart policy (`no`, `on-failure`, `always`)
-   Type= → startup type (`simple`, `forking`, `oneshot`, `notify`, `dbus`)
-   User= / Group= → specify which user/group the service should run as (non-root recommended)

[Install] = Defines how the unit is enabled/disabled at boot
Common directive:

-   WantedBy → target that pulls this unit in
-   RequiredBy → stronger form of dependency
