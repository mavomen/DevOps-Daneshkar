---
id: LanSetup
aliases: []
tags: []
---

# LAN Setup

Configure a local area network.

## Basic Network Design

```
Internet → Router → Switch → Servers/Workstations
           192.168.1.1   192.168.1.0/24
```

## Static IP Assignment

```bash
# Server with static IP
sudo ip addr add 192.168.1.10/24 dev eth0
sudo ip route add default via 192.168.1.1

# DNS configuration
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
```

## DHCP Server Setup

```bash
# Install DHCP server
sudo apt install isc-dhcp-server

# Configure /etc/dhcp/dhcpd.conf
subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.100 192.168.1.200;
    option routers 192.168.1.1;
    option domain-name-servers 8.8.8.8;
}
```

## Firewall Rules

```bash
# Allow internal traffic
sudo iptables -A INPUT -i eth0 -s 192.168.1.0/24 -j ACCEPT
sudo iptables -A INPUT -i eth0 -j DROP
```

## Related Notes

- [[IpAddresses]] - IP addressing
- [[RoutingTables]] - Routing configuration
- [[NetworkSecurity]] - Security hardening
