---
id: NetworkingBasics
aliases: []
tags: []
---

# Networking Basics

Linux networking: interfaces, routing, DNS, and firewall.

## View Network Info

```bash
ip addr show                                # IP addresses
ip link show                                # Network interfaces
ip route show                               # Routing table
cat /etc/resolv.conf                        # DNS config
ss -tlnp                                    # Listening ports
ss -tnp                                     # Active connections
```

## Interface Configuration

```bash
ip addr add 192.168.1.100/24 dev eth0        # Add IP
ip link set eth0 up                         # Bring up
ip link set eth0 down                       # Bring down
ip route add default via 192.168.1.1        # Default gateway
```

## DNS

```bash
dig example.com                             # DNS lookup
dig +short example.com                      # Quick IP
nslookup example.com                        # Basic DNS
host example.com                            # Simple lookup
cat /etc/resolv.conf                        # DNS servers
```

## Common Tools

```bash
ping -c 4 8.8.8.8                           # Test connectivity
traceroute google.com                       # Trace path
curl -I https://example.com                 # HTTP headers
wget https://example.com/file               # Download
scp file.txt remote:/path/                  # Copy over SSH
```

## Firewall

```bash
sudo ufw status verbose                     # UFW status
sudo ufw allow 80/tcp                       # Allow port
sudo iptables -L -n                         # List raw rules
sudo nft list ruleset                        # nftables
```

## Related Notes

- [[ip]] — ip command
- [[ss]] — ss command
- [[ping]] — ping command
- [[NetworkIssues]] — Network troubleshooting
