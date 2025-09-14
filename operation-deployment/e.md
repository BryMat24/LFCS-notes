# SELinux MAC

---

Fine grained control.

Installed via: selinux-basics, setools-console, auditd - allows to monitors

```
ls -Z # see context for files
ps axZ # see context for processes
id -Z # see context for user
sudo semanage login -l  # see mapping of SElinux user when login
sudo semanage user -l # see what role can user assume
getenforce  # see if selinux is enabled
```

to change the mode for selinux permanently, set it in the /etc/selinux/config

## SELinux context:

\<user>:\<role>:\<type>:\<level>

-   user = every user is mapped to this SELinux user
-   role = each user can only assume certain roles, a role is a mapping between user and the type
-   type = defines the permission of what this user / process can do
-   level = ignore this

## Steps

setup

```
sudo apt install auditd selinux-basics
sestatus
sudo selinux-activate
```

audit2why

explains SELinux denials in plain language, It parses log messages from the audit logs (/var/log/audit/audit.log) or from dmesg when SELinux blocks something. Instead of showing cryptic AVC messages, it tells you why access was denied.

```
sudo audit2why --all | less
sudo audit2allow -all -M mymodule # generate custom SELinux policy module
semodule -i mymodule.pp # adds the new SELinux policy module
```

chcon

change selinux context

```
chcon -u unconfined_u /var/log/auth.log
chcon -r object_r /var/log/auth.log
chcon -t user_home_t /var/log/auth.log
chcon --reference=/var/log/syslog /var/log/auth.log # copy context from one reference and copy it to the target file
```

seinfo

to see the available context labels

```
seinfo -u
seinfo -r
seinfo -t
```

restorecon

restore file SELinux contexts (labels) to their defaults. It looks up the correct context from the SELinux policy (file_contexts) and re-applies it to files/directories.

SeLinux has a policy context DB,
eg. /var/www(/.\*)? system_u:object_r:httpd_sys_content_t:s0
Means: any file under /var/www/ should get httpd_sys_content_t.

```
mv /tmp/index.html /var/www/html/
ls -Z /var/www/html/index.html   # shows wrong type (tmp_t)
restorecon -v /var/www/html/index.html
ls -Z /var/www/html/index.html   # fixed to httpd_sys_content_t
```

We can see the default file context DB using the following command

```
sudo semanage fcontext --list
sudo semanage fcontext --add --type "nfs_t" "/nfs/shares(/.*)?"
```

booleans

```
sudo setsebool virt_use_nfs 1
sudo getsebool virt_use_nfs
```

ports

```
sudo semanage port --list # see which port certain daemon can bind to
sudo semanage port --add --type ssh_port_t --proto tcp 2222
```
