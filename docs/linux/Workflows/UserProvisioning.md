---
id: UserProvisioning
aliases: []
tags: []
---

# User Provisioning — Workflow

Creating and configuring user accounts.

## New User Setup

```bash
# 1. Create user with home directory
useradd -m -s /bin/bash alice

# 2. Set password
passwd alice

# 3. Add to groups
usermod -aG wheel alice                    # Sudo access
usermod -aG docker alice                   # Docker access
usermod -aG developers alice               # Project group

# 4. Set up SSH
mkdir -p /home/alice/.ssh
chmod 700 /home/alice/.ssh
# Add public key
chown -R alice:alice /home/alice/.ssh
```

## User Configuration Checklist

- [ ] Home directory created
- [ ] Correct shell set
- [ ] Groups assigned
- [ ] Password set
- [ ] SSH keys configured
- [ ] sudo access (if needed)
- [ ] No unnecessary privileges

## Bulk Provisioning

```bash
# From CSV file
while IFS=, read -r name group shell; do
    useradd -m -s "$shell" "$name"
    usermod -aG "$group" "$name"
    echo "$name:$(openssl rand -base64 12)" | chpasswd
done < users.csv
```

## User Removal

```bash
# Kill processes, move files, delete
pkill -u alice
userdel -r alice                           # Remove user + home dir
```

## Related Notes

- [[UserAccountInvestigation]] — User investigation
- [[UsersAndGroups]] — User management
- [[GroupInvestigation]] — Group management
- [[EtcPasswd]] — /etc/passwd
