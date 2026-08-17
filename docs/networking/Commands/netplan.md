---
id: netplan
aliases: []
tags: []
---

# netplan

Ubuntu's network configuration utility. Writes YAML config files that generate backend configs (NetworkManager or systemd-networkd).

## Config files

```bash
# Location
ls /etc/netplan/

# Typical file
cat /etc/netplan/01-config.yaml
```

## Static IP example

```yaml
# /etc/netplan/01-config.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      addresses:
        - 192.168.1.100/24
      routes:
        - to: default
          via: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4
```

## DHCP example

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: true
```

## Multiple interfaces

```yaml
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: false
      addresses:
        - 10.0.0.10/24
      routes:
        - to: default
          via: 10.0.0.1
    eth1:
      dhcp4: true
```

## Apply changes

```bash
# Test configuration (auto-reverts in 120s)
sudo netplan try

# Apply immediately
sudo netplan apply

# Generate backend configs without applying
sudo netplan generate
```

## When to use

- Ubuntu 17.10+ (default network config tool).
- Server and desktop environments on Ubuntu.

## Related Notes

- [[Commands/nmcli|nmcli]]
- [[Commands/ip|ip]]
- [[IpAddresses]]
