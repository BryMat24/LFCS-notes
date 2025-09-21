# Configure IPV4 & IPV6

---

Temporary change to network interface

```
ip link    # See network devices, physical or virtual
ip -c a    # see the IP address of each of these network interfaces
ip link set dev <name> up # bring network interface up
ip addr add <IP> dev <name> # add network address to the network interface
ip addr delete <IP> dev <name> # delete network address of network interface
ip route
```

Permanent network interace change setting

/etc/netplan contain yaml files that defines network configurations

```
sudo netplan get
sudo netplan try # able to rollback chnages applied to netplan
man netplan # see what we can write in the config file
ls /usr/share/doc/netplan/examples # contain example in configuring various parts of netplan components
```

DNS resolver

```
vim /etc/systemd/resolved.conf
sudo systemctl restart systemd-resolved.service
```

## Socket Statistics

Display information about sockets, which are endpoint of communication

```
ss -tulnp
```

-l listening (show listening sockets)
-t tcp
-u udp
-n numeric
-p what process is involved for each entry of output
