---
id: FirewallRules
aliases: []
tags: []
---

# Firewall Rules

Configure firewall rules for network security.

## iptables Basics

```bash
# View rules
sudo iptables -L -n -v

# Allow established connections
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Allow SSH
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Allow HTTP/HTTPS
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Drop everything else
sudo iptables -P INPUT DROP

# Save rules
sudo iptables-save > /etc/iptables/rules.v4
```

## UFW (Uncomplicated Firewall)

```bash
# Enable UFW
sudo ufw enable

# Default policies
sudo ufw default deny incoming
sudo ufw default allow outgoing

# Allow services
sudo ufw allow ssh
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# Rate limiting
sudo ufw limit ssh

# View status
sudo ufw status verbose
```

## nftables (Modern Replacement)

```bash
# List ruleset
sudo nft list ruleset

# Add rules
sudo nft add rule inet filter input tcp dport 22 accept
sudo nft add rule inet filter input tcp dport {80, 443} accept
```

## Related Notes

- [[NetworkSecurity]] - Security hardening
- [[LanSetup]] - LAN firewall rules
- [[TroubleshootingConnectivity]] - Connection issues
