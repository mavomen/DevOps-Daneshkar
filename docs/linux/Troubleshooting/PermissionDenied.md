---
id: PermissionDenied
aliases: []
tags: []
---

# Permission Denied — Troubleshooting

Common permission issues and fixes.

## Quick Diagnosis

```bash
ls -la file                                # Check permissions and ownership
namei -l /path/to/file                     # Full path permissions
id username                                # User's groups
groups username                            # Group membership
stat file                                  # Detailed file info
```

## Common Fixes

### File/Directory Permission

```bash
chmod 755 script.sh                        # Make executable
chmod +x script.sh                         # Add execute
chmod -R 644 /var/www/                     # Set recursively
chmod -R 755 /var/www/html/                # Directories executable
```

### Ownership

```bash
chown user:group file                      # Change owner
chown -R www-data:www-data /var/www        # Recursive
chown :docker file                         # Change group only
```

### SSH Key Permissions

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
chmod 600 ~/.ssh/authorized_keys
```

### Sudo Issues

```bash
# User not in sudo group
usermod -aG wheel alice

# Command not allowed
visudo                                      # Check sudoers
sudo -l                                    # View allowed commands
```

## SELinux / AppArmor

```bash
# SELinux
getenforce                                 # Check mode
setenforce 0                               # Permissive (temporary)
ls -laZ file                               # Check context
restorecon -Rv /var/www                    # Fix contexts

# AppArmor
aa-status                                  # Check profiles
sudo aa-complain /usr/sbin/nginx           # Set complain mode
```

## Related Notes

- [[LinuxPermissions]] — Permission concepts
- [[UserAccountInvestigation]] — User investigation
- [[SudoConfiguration]] — Sudo config
- [[SecurityHardening]] — Security best practices
