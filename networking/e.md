# Configure SSH Servers and Clients

---

### **Server**

Configuring SSH Server

```
sudo apt update && sudo apt install openssh-server -y

sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh

sudo vim /etc/ssh/sshd_config   # main config file for SSH daemon
sudo systemctl reload ssh.service
```

### **Client**

```
man ssh_config  # configure ssh config for client

vim .ssh/config # client ssh config in .ssh/config, store connection to servers
```

Specific user settings for SSH client

```
(file content)
Host ubuntu-vm
        Hostname 10.0.0.186
        Port 22
        User jeremy

chmod 600 ~/.ssh/config
```

Global setting for SSH client

```
sudo vim /etc/ssh/ssh_config
```

### **Key Pair Login**

Client

```
ssh-keygen # generate key pair in client

ssh-copy-id <user>@<ip> # copy the public key to the authorized_keys in .ssh folder in server
```
