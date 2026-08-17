---
id: NetworkInterfaces
aliases: []
tags: []
---

# Network Interfaces

Configure and manage network interfaces on Linux.

## View Interfaces

```bash
ip addr show                                # Show all interfaces
ip link show                                # Show link layer info
ifconfig                                    # Legacy interface display
ethtool eth0                                # Interface details
```

## Configure Interface

```bash
# Temporary configuration
sudo ip addr add 192.168.1.100/24 dev eth0
sudo ip link set eth0 up

# Permanent (Debian/Ubuntu) - /etc/network/interfaces
auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1

# Permanent (RHEL/CentOS) - /etc/sysconfig/network-scripts/ifcfg-eth0
TYPE=Ethernet
BOOTPROTO=static
IPADDR=192.168.1.100
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
ONBOOT=yes
```

## Related Notes

- [[IpAddresses]] - IP addressing
- [[RoutingTables]] - Routing configuration
- [[TroubleshootingConnectivity]] - Connectivity issues
