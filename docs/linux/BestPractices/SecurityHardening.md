---
id: SecurityHardening
aliases: []
tags: []
---

# Linux Security Hardening — Best Practices

Essential security measures for Linux systems.

## User & Access Control

- **Disable root login** via SSH (`PermitRootLogin no`)
- **Use key-based auth** (`PasswordAuthentication no`)
- **Run as non-root** wherever possible
- **Enforce strong passwords** (`pam_pwquality`)
- **Use sudo** instead of su

```bash
# Create deploy user with sudo
useradd -m -s /bin/bash deploy
usermod -aG wheel deploy
```

## SSH Hardening

```bash
Port 2222
AllowUsers deploy
MaxAuthTries 3
ClientAliveInterval 300
```

## File Permissions

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
chmod 644 /etc/passwd
chmod 640 /etc/shadow
chmod 440 /etc/sudoers
```

## Service Minimization

```bash
systemctl list-units --type=service --state=running  # Audit running services
systemctl disable --now avahi-daemon                 # Disable unused services
systemctl disable --now cups                         # Disable printing if unused
```

## Firewall

```bash
ufw default deny incoming
ufw default allow outgoing
ufw allow ssh
ufw allow 80/tcp
ufw allow 443/tcp
ufw enable
```

## Kernel Hardening

```bash
# /etc/sysctl.d/99-security.conf
net.ipv4.conf.all.rp_filter=1             # Reverse path filtering
net.ipv4.icmp_echo_ignore_broadcasts=1    # Ignore broadcast pings
net.ipv4.conf.all.accept_redirects=0      # Reject redirects
kernel.randomize_va_space=2               # ASLR full randomization
fs.suid_dumpable=0                        # No core dumps for SUID
```

## Audit & Monitoring

```bash
# Install and enable auditd
sudo apt install -y auditd
systemctl enable --now auditd

# Key files to audit
auditctl -w /etc/passwd -p wa -k passwd
auditctl -w /etc/shadow -p wa -k shadow
auditctl -w /etc/sudoers -p wa -k sudoers
```

## Related Notes

- [[SshdConfig]] — SSH server config
- [[EtcSudoers]] — Sudo rules
- [[LinuxPermissions]] — File permissions
- [[FirewallRules]] — Firewall config
- [[SystemStatus]] — System investigation
