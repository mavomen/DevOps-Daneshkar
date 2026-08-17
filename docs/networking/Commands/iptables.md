---
id: iptables
aliases: []
tags: []
---

# iptables

Linux firewall tool that configures Netfilter kernel rules for packet filtering and NAT.

## Chain structure

```
Incoming packet → INPUT chain → local process
                 FORWARD chain → forwarded to another interface
Outgoing packet ← OUTPUT chain
```

## Common commands

```bash
# List all rules
sudo iptables -L -n -v

# Allow SSH
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Allow HTTP/HTTPS
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Block a specific IP
sudo iptables -A INPUT -s 10.0.0.50 -j DROP

# Allow established connections
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Default policy: deny all incoming
sudo iptables -P INPUT DROP

# Delete a rule
sudo iptables -D INPUT -s 10.0.0.50 -j DROP

# Insert at position 1
sudo iptables -I INPUT 1 -p tcp --dport 8080 -j ACCEPT

# Flush all rules
sudo iptables -F
```

## Options

| Option | Purpose |
|---|---|
| `-A` | Append rule to chain |
| `-I` | Insert rule at position |
| `-D` | Delete rule |
| `-F` | Flush (delete all) rules |
| `-L` | List rules |
| `-P` | Set default policy |
| `-n` | Numeric output (no DNS) |
| `-v` | Verbose |

## Targets

| Target | Action |
|---|---|
| ACCEPT | Allow packet |
| DROP | Silently discard |
| REJECT | Discard with error response |
| LOG | Log packet and continue |

## Notes

- `iptables` rules are lost on reboot — use `iptables-persistent` or `netfilter-persistent` to save.
- Consider `ufw` for simpler syntax on Ubuntu.

## Related Notes

- [[Commands/firewalld|firewalld]]
- [[Firewall]]
- [[NatAndPAT]]
