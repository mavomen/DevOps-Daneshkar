---
id: NetworkConfiguration
aliases: []
tags: []
---

# Network Configuration

Overview of Linux network configuration methods.

## Configuration Methods

| Method | Use Case | Config Location |
|--------|----------|-----------------|
| Netplan | Ubuntu 18.04+ | `/etc/netplan/` |
| NetworkManager | Desktop Linux | `nmcli`, GUI |
| systemd-networkd | Servers | `/etc/systemd/network/` |
| ifupdown | Legacy Debian | `/etc/network/interfaces` |
| ip command | Temporary | Immediate effect |

## View Current Configuration

```bash
ip addr show                              # IP addresses
ip route show                             # Routes
cat /etc/resolv.conf                      # DNS
nmcli device status                       # NetworkManager status
```

## Related Notes

- [[ResolvConf]] — DNS configuration
- [[NetworkInterfaces]] — Interface setup
- [[SysctlNetworking]] — Kernel parameters
