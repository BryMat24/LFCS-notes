# Port Forwarding & NAT

---

port fowarding = is a networking technique where traffic coming into a system on one port is forwarded to another port, often on the same machine or a different one. Redirects traffic from public IP:port to private IP:port. (special case of NAT focused on port)

NAT = General technique of rewriting IP addresses (and sometimes ports) as packets pass through a router/firewall. It allows: 1) Allow many private devices to share one public IP (SNAT/PAT), 2) Hide internal IPs

```
sudo vim /etc/sysctl.d/99-sysctl.conf # enable net.ipv4.ip_forward = 1
sudo sysctl --system # reload
sudo sysctl -a | grep forward # check if already applied
```

### iptables (NAT / port forward)

-   works at the Netfilter level, not just routing
-   it can rewrite packets not just routing, changing the destination IP/port
-   works by chains, and works through processes added on those chains

```
sudo iptables -t nat -A PREROUTING -i <interface> -s 10.0.0.0/24 -p tcp -dport 8080 -j DNAT --to-destination 192.168.1.50:80
```

This changes the destination of the packet so that routing uses the new address

-   -t = table
-   -A = chain
-   -i = input interface
-   -s = source IP
-   -p = tcp/udp
-   -dport = dest port
-   -j DNAT

```
sudo iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -o enps6s0 -j MASQUERADE
```

This replaces the source IP with its own IP dynamically.

```
sudo apt install iptables-persistent
sudo netfilter-persistent save

```

This is to make changes persistent.

```
man ufw-framework
sudo iptables --list-rules --table nat
```

docs
