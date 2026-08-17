---
id: 03-InfrastructureMOC
aliases: []
tags: []
---

# Infrastructure (MOC)

Routing, gateways, NAT, topologies, and network configuration.

## Concepts

- [[RoutingAndGateways|Routers & Gateways]]
- [[NatAndPAT|NAT & PAT]]
- [[NetworkTopology|Network Topology]]
- [[Subnetting|Subnetting]]

## Commands

- [[Commands/netplan|netplan]] — Ubuntu network config
- [[Commands/nmcli|nmcli]] — NetworkManager CLI
- [[Commands/ip|ip]] — modern network config

## Configuration

- [[ResolvConf]] — DNS resolver configuration
- [[NetworkInterfaces]] — Interface configuration
- [[SysctlNetworking]] — Kernel networking parameters

## Workflows

- [[LanSetup]] — Local area network setup
- [[VpnSetup]] — VPN configuration
- [[FirewallRules]] — Firewall configuration

## Configure a static IP

```yaml
# Netplan (Ubuntu)
network:
  version: 2
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
```

```bash
sudo netplan try    # test (auto-reverts in 120s)
sudo netplan apply  # apply immediately
```

## Related Notes

- [[00-Networking|Networking Overview]]
