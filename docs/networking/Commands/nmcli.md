---
id: nmcli
aliases: []
tags: []
---

# nmcli

NetworkManager Command-Line Interface. Configures and manages network connections on Linux.

## Show connections

```bash
# List all connections
nmcli connection show

# Show specific connection
nmcli connection show "Wired connection 1"

# Show active connections
nmcli connection show --active
```

## Manage connections

```bash
# Bring connection up
nmcli connection up "Wired connection 1"

# Bring connection down
nmcli connection down "Wired connection 1"

# Delete connection
nmcli connection delete "Wired connection 1"
```

## Configure IP

```bash
# Set static IP
nmcli connection modify "Wired connection 1" \
  ipv4.addresses 192.168.1.100/24 \
  ipv4.gateway 192.168.1.1 \
  ipv4.dns "8.8.8.8 8.8.4.4" \
  ipv4.method manual

# Set DHCP
nmcli connection modify "Wired connection 1" \
  ipv4.method auto

# Apply changes
nmcli connection up "Wired connection 1"
```

## Device status

```bash
# Show network devices
nmcli device status

# Show device details
nmcli device show eth0
```

## When to use

- Desktop environments with NetworkManager.
- Systems where `netplan` delegates to NetworkManager.
- Quick connection management without editing config files.

## Related Notes

- [[Commands/netplan|netplan]]
- [[Commands/ip|ip]]
- [[IpAddresses]]
