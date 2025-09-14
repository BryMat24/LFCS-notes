## Package Managers

---

### 1. 🔹 APT (Debian, Ubuntu)

Update & install

```
apt update && apt install nginx
```

Low-level dpkg usage

```
dpkg --listfiles nginx        # list installed files from package
dpkg --search /usr/sbin/nginx # find package owning a file
```

Search & inspect

```
apt show libnginx-mod-stream     # show package details
apt search nginx                 # search descriptions
apt search --names-only nginx    # search by name only
```

Remove packages

```
apt remove nginx       # remove package (keep dependencies)
apt autoremove         # remove unused dependencies
apt autoremove nginx   # remove package and its dependencies
```

### 2. Configure Repositories

Files /etc/apt/sources.list, /etc/apt/sources.list.d/\*.list (third-party repos)

```
curl -fsSL https://download.example.com/docker.gpg -o docker.key
gpg --dearmor docker.key
sudo mv docker.key.gpg /etc/apt/keyrings/docker.gpg
```

```
deb [signed-by=/etc/apt/keyrings/docker.gpg] https://download.example.com stable main
```

```
apt update
```

### 3. Install from source

```
./configure
make # compile
sudo make install # move the compiled things to the /usr/bin to be executable
```
