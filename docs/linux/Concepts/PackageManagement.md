---
id: PackageManagement
aliases: []
tags: []
---

# Package Management

Installing, updating, and removing software packages on Linux.

## Package Managers by Distro

| Distro | Manager | Install | Remove | Search | Update |
|--------|---------|---------|--------|--------|--------|
| Debian/Ubuntu | apt | `apt install pkg` | `apt remove pkg` | `apt search pkg` | `apt update && apt upgrade` |
| Arch | pacman | `pacman -S pkg` | `pacman -R pkg` | `pacman -Ss pkg` | `pacman -Syu` |

## Common Operations

```bash
# Debian/Ubuntu
sudo apt update                             # Refresh package list
sudo apt upgrade                            # Upgrade all packages
sudo apt install nginx                      # Install package
sudo apt remove nginx                       # Remove (keep config)
sudo apt purge nginx                        # Remove (delete config)
sudo apt autoremove                         # Remove unused deps
dpkg -l | grep nginx                        # Check if installed

# Arch
sudo pacman -Syu                            # Full system upgrade
sudo pacman -S nginx                        # Install
sudo pacman -R nginx                        # Remove
pacman -Qs nginx                            # Check if installed
```

## Related Notes

- [[SystemUpdates]] — Update workflows
- [[SystemdAndInit]] — Service management
- [[SecurityHardening]] — Keeping systems updated
