# Network

---

## Bridge and Bond

**Bridge** - A virtual switch that connects multiple network interfaces at layer 2. Treat our computer like a network switch. We bridge multiple NIC, so traffic coming from one NIC can be routed to the other NIC. We assign IPs on the bridge itself not the NICs.

**Bonding** - Treat multiple NIC as if one NIC (from software perspective), so application can receive network packets with more bandwidth and higher redundancy. (not all modes increase network throughput, only mode 4 can)

Bonding Modes (mode 0 - 6)

-   Mode 0 = round robin, keep on exchanging which NIC to use
-   Mode 1 = active backup, only use 1 NIC, and use other as backups
-   Mode 2 = XOR, picks which NIC to use based on destination and source, so always same NIC for a particular source / dest pair
-   Mode 3 = Broadcast, send to all NIC at once
-   Mode 4 = Increase network transfer rates compared to what a single interface can support
-   Mode 5 = Adaptive transmit load-balancing, least busy interface (outgoing traffic), send data from least busy interface
-   Mode 6 = Adaptive load-balancing, both outgoing and ingoing traffic

## Squid

**Squid** - Open Source Caching Proxy Server (forward-proxy), sits between client and server, and can:

-   Cache frequently requested content (reduce bandwidth, speed up responses).
-   Filter traffic (block sites, restrict protocols).
-   Control access (ACLs, authentication).
-   Forward traffic (act as a proxy or reverse proxy).

```
# 1. install squid
sudo apt install squid -y

# 2. Edit config /etc/squid/squid.conf

# 3. setup acl

# 4. to connect internet via squid from another computer, can do export http_proxy=http://10.0.0.2:3128 or can do curl -x <proxy_url> -L <target_url>

sudo tail -f /var/log/squid/access.log
```

In Squid, http_access controls whether a client is allowed to use the proxy for a request at all. It is not limited to HTTP websites only.

## Packet Filtering & Firewall

ufw tool, to allow/deny from target and control certain ports

Syntax Pattern

if a component is not specified, it assumes from everywhere

```
ufw allow|deny [in|out] [on <iface>] \
   [from <IP/subnet>] [to <IP>] [port <num>] [proto tcp|udp]
```

Basics

```
sudo ufw status numbered
sudo ufw enable
```

IP specific

```
# Allow specific IP
sudo ufw allow from 192.168.1.50

# Allow entire subnet
sudo ufw allow from 192.168.1.0/24

# Allow IP to specific port
sudo ufw allow from 192.168.1.50 to any port 22

# Deny specific IP
sudo ufw deny from 10.0.0.100
```

Inserts based on ranks

```
sudo ufw delete <rule_number>
sudo ufw insert <rule_number> deny from <IP> # allow to insert with certain rule rank
```

Interface-specific profiles

```
# Allow traffic to port 80 only on eth0
sudo ufw allow in on eth0 to any port 80

# Allow traffic from subnet on eth1
sudo ufw allow in on eth1 from 192.168.2.0/24
```

Outgoing network (need to specify 'out')

```
sudo ufw allow out 53/udp       # Allow outbound DNS queries
sudo ufw deny out 25/tcp        # Block outbound SMTP (stop spam)
sudo ufw allow out to 8.8.8.8 port 53 proto udp
```
