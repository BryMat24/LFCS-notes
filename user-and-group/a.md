# User Management

---

### Understanding User Accounts

System users: UID < 1000 (or < 500 in some distros). Created for daemons/services.

Regular users: UID ≥ 1000.

Account details stored in:

-   /etc/passwd → usernames, UID, GID, home dir, shell.

-   /etc/shadow → password hashes, expiration settings.

-   /etc/group → group definitions.

useradd parameters:

-   -c Any text string. It is generally a short description of the login, and is currently used as the field for the user's full name.
-   -e date after which the/ user will be disabled
-   -g primary group. NOTE: if not specified it will be created a new group with same name of user that will be become user's primary group
-   -G secondary groups
-   -m create home directory. Useless because CREATE_HOME is yes
-   -p configure password. NOTE: value must be provided encrypted
    Normally password is not provided during user add
-   -s shell to use

usermod

used to modify a user

```
sudo usermod -aG wheel bob
sudo usermod -s /bin/zsh bob
sudo usermod -d /home/newbob bob
```

delete user

```
sudo userdel bob
sudo userdel -r bob # delete acc + home dir
```

password

```
sudo passwd bob
```

groups

```
sudo groupadd developers
sudo groupdel developers
groups bob
```

expire dates

```
sudo chage -d 0 jane
```

skeleton directory /etc/skel/

```
echo "Welcome" > /etc/skel/README.txt
useradd -m alice
cat /home/alice/README.txt
```

/etc/profile.d = directory contains scripts or files that are sourced when login shell for all users
/etc/environment = system-wide env variables

### Managing resource limits for user

ulimit

It limits the use of system-wide resources

Limits can be configured changing file /etc/security/limits.conf

Typical configuration

```
1. @student        hard    nproc           20
2. @faculty        soft    nproc           20
3. ftp             hard    nproc           0
4. @student        -       maxlogins       4
```

-   Members of student group can run only 20 processes
-   Members of faculty group will receive and info after that more than 20 processes were run (soft limit)
-   ftp user cannot run any process
-   Members of student can have maximum 4 logged user. - means both hard and soft
    man limits.conf for manual

man limits.conf for manual, Also ulimit command can be used to change limits

Temporary Limits (per shell/session)

```
ulimit -n 2048       # max open files for this shell
ulimit -t 120        # CPU time in seconds
ulimit -u 100        # max number of processes
```

sudoers
File location: /etc/sudoers

```
visudo
```

syntax of /etc/sudoers

```
<user_or_group>   <hosts>=<runas>   <commands>
```

### LDAP

1. cat /etc/passwd
2. id john
3. installing ldap serve with lxc and install libnss-ldapd
4. cat /etc/nsswitch.conf (ldaps added to 3 lines in that file)
5. cat /etc/nslcd.conf (points to ldap server)
6. get all users: getent passwd

```
getent passwd --service ldap
getent group --service ldap
```

7. PAM: to create user direct

```
pam-auth-udpate
```
