# Linux Security Incident Response

As an incident responser, you should always be aware of what **should be** & what **should not** be present in your systems.

The security incidents that could be overcome by:

- By examiining the running processes
- By having insights into the contents of physical memory
- By gathering details on the hostname, IP address, OSs, etc.
- Gathering information on system services
- By identifying all the known & unknown users logged onto the systems
- By inspecting network connections, open ports & any network activity
- By determining the various files present

## User Accounts

Investigate the user accounts' acttivity to understand:

- logged-in users
- existing users
- usual/un-usual logins
- failed login attempts
- permissions
- access by sudo
- etc.

### `/etc/passwd`

To fetch all the info about user accounts:

```sh
❯ cat /etc/passwd
root:x:0:0::/root:/usr/bin/bash
bin:x:1:1::/:/usr/bin/nologin
daemon:x:2:2::/:/usr/bin/nologin
mail:x:8:12::/var/spool/mail:/usr/bin/nologin
ftp:x:14:11::/srv/ftp:/usr/bin/nologin
http:x:33:33::/srv/http:/usr/bin/nologin
nobody:x:65534:65534:Kernel Overflow User:/:/usr/bin/nologin
dbus:x:81:81:System Message Bus:/:/usr/bin/nologin
systemd-timesync:x:974:974:systemd Time Synchronization:/:/usr/bin/nologin
mava:x:1000:1000::/home/mava:/bin/zsh
git:x:966:966:git daemon user:/:/usr/bin/git-shell
nvidia-persistenced:x:143:143:NVIDIA Persistence Daemon:/:/usr/bin/nologin
systemd-imds:x:965:965:systemd Instance Metadata:/:/usr/bin/nologin
postgres:x:963:963:PostgreSQL user:/var/lib/postgres:/usr/bin/bash
```

The format of each line is:
`username:password(placeholder):UID:GID:GECOS(description):home_directory:login_shell`

| Username                | Translation / What it is                                                                                                             |
| :---------------------- | :----------------------------------------------------------------------------------------------------------------------------------- |
| **root**                | The superuser / system administrator. Has full control. Uses `/usr/bin/bash` as its shell.                                           |
| **bin**                 | Legacy system user - historically owned binary commands. No login (nologin).                                                         |
| **daemon**              | Legacy user for background system services. No login.                                                                                |
| **mail**                | Owns the mail spool directory (`/var/spool/mail`). Handles email storage. No login.                                                  |
| **ftp**                 | Used by the FTP server. Home is `/srv/ftp`. No login.                                                                                |
| **http**                | Used by the web server (Apache / Nginx / etc.) to serve files. Home is `/srv/http`. No login.                                        |
| **nobody**              | The “lowest‑privilege” user - used for processes that need almost no permissions. Description says “Kernel Overflow User”. No login. |
| **dbus**                | Runs the D‑Bus message bus system (used for inter‑process communication). No login.                                                  |
| **mava**                | **This is your personal user account.** UID 1000, home `/home/mava`, shell `/bin/zsh`.                                               |
| **git**                 | The Git daemon user - allows anonymous Git access over SSH (shell is `/usr/bin/git-shell`, which restricts login to Git commands).   |
| **nvidia-persistenced** | Keeps the NVIDIA GPU driver loaded and active, even when no programs are using it. No login.                                         |
| **systemd-imds**        | systemd Instance Metadata - fetches cloud instance metadata (AWS, Azure, etc.). No login.                                            |
| **postgres**            | The user for the PostgreSQL database server. Has a real shell (`/usr/bin/bash`) and home `/var/lib/postgres`.                        |
| **valkey**              | The user for Valkey (a Redis‑compatible in‑memory data store). No login.                                                             |
| **mattermost**          | The user for the Mattermost team‑chat server. No login.                                                                              |

NOTE:

- Only **root** and **mava** (and **postgres**) have a real login shell (`bash` or `zsh`) in this list - the rest are _system users_ that run background services and cannot be used to log in interactively.
- Your own account is **mava** (UID 1000) with Zsh as your shell.

The `setuid` option in linux is unique file permission. So, on a Linux system when a user wants to make the change of password, they can run the `passwd` command. As the root account is marked as setuid, you can get temporary permission.

```sh
❯ passwd -S mava
mava P 2026-06-23 0 99999 7 -1
```

The output format is:
`username:status:last_change:min:max:warn:inactive`

| Field                    | Value        | Meaning                                                                                                                                                            |
| :----------------------- | :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Username**             | `mava`       | Your account.                                                                                                                                                      |
| **Password status**      | `P`          | **P** = usable password (the account has a valid password set and it works). Other possible letters: `L` (locked), `NP` (no password), `PK` (password is expired). |
| **Last password change** | `2026-06-23` | You last changed your password on **June 23, 2026**. (That’s about 5 weeks ago from today, July 28, 2026).                                                         |
| **Minimum days**         | `0`          | You can change your password **any time** - there’s no mandatory waiting period between changes.                                                                   |
| **Maximum days**         | `99999`      | Your password is valid for **~273 years** (99999 days) before it forces you to change it. In practice, this means **it never expires**.                            |
| **Warning period**       | `7`          | If your password _did_ have an expiry, you’d get a warning **7 days in advance**. Since it doesn’t expire, this doesn’t matter.                                    |
| **Inactivity period**    | `-1\*\*      | **No inactivity timer** - your account will never be automatically disabled just because you haven’t logged in for a while.                                        |

### `grep`

Grep is used for _searching plain-text foor lines that match a regular expression (regex). `:0:` is used to **display `UID 0` files in `/etc/passwd` file**_.

```sh
❯ grep :0: /etc/passwd
root:x:0:0::/root:/usr/bin/bash
# the translation is same as earlier
```

### `find /-nouser -print`

To identify & display whether an attacker created any temporary user to perform an attack, initiating account backdoors, etc.

This command scans your entire filesystems for _files & directories that have no valid owner_

- So, practically the numeric UIDs attached to the file does **not** exist in your `/etc/passwd` file.

```sh
Linux (main) U
❯ sudo find / -nouser -print
find: ‘/proc/97989’: No such file or directory
find: ‘/proc/102412/task/102412/fd/6’: No such file or directory
find: ‘/run/user/1000/gvfs’: Permission denied
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/390/fs/opt/yarn-v1.22.22/lib
/mnt/hdd/VMs/ubuntu-23.04-desktop-amd64.iso
```

> `/proc` is a virtual filesystem for running processes.

1. The Errors (Ignore these - they're harmless)

- `find: ‘/proc/97989’: No such file or directory` - process ended in the split second between `find` listing the directory & trying to inspect it. (Normal, ignore...)
- `Permission denied` for `/run/user/1000/doc` and `/run/user/1000/gvfs` - These are FUSE/mount points used by your desktop session (GVFS). Even `root` can't always peek inside them because they're restricted by the mount type. (Normal, ignore...)

2. The Actual "Orphaned" Files (Grouped)

- The _Containerd_ (container-d) snapshot files (the huge list under `/var/lib/containerd/...`)
  Your system has Docker or `containerd` running. These files live inside _overlay snapshot layers_ used by containers.

- Why are they `nouser`?
  Inside a container, a file might be owned by UID `1000` (for an `app` user). But on your _host_ machine:
  - that specific numeric UID might be mapped to a different sub-UID (e.g., `100000`) by user namespace remapping
  - it belongs to a UID that simply doesn't have an entry in your host's `/etc/passwd`. Since the host doesn't recognize that UID, `find` flags them as orphaned.

- What are these specific files?
  - Yarn (the JavaScript package manager) installed inside a container.
  - A home directory for a user named `app` inside a container (with `.bashrc`, `.profile`).
  - Partial APT cache folders (`/var/cache/apt/archives/partial`) **inside a container**.

Verdict: **Totally normal.** These are internal container layers.

> [!WARNING] Do NOT delete them manually
> if you need to reclaim space, use `docker system prune` or `nerdctl system prune` to let Docker/containerd clean up unused layers properly.

3. he ISO files under `/mnt/hdd/VMs/`

It is **NOT** inside containers. They are directly on your HDD in a `VMs` directory.

- Why are they `nouser`?
  They are owned by a numeric UID that no longer exists in your current `/etc/passwd`. Since we only see `mava` (UID 1000) and system users, this UID was probably:
  - A previous user account you deleted (e.g., an old `vmuser` or `app` user with UID 1001, 1002, etc.).
  - Or they were copied over from another machine/backup where the user had a different UID.

- What should you do?

- Check the actual numeric UID of those ISO files:
  Run: `ls -n /mnt/hdd/VMs/`
  (The `-n` flag shows numeric UIDs instead of names). This will tell you exactly which UID owns them (e.g., `1001`).

- If you want to take ownership (so they stop showing up as `nouser`), run: `sudo chown -R mava:mava /mnt/hdd/VMs/`
  (Replace `mava` with whoever should own them - probably you).

- For the containerd files: they are safe to ignore. If they bother you visually, remember that they're just container layers. Only delete them via the container runtime's pruning commands to avoid breaking running containers.

#### Summary in plain English

> **Translation:** Your system has no missing user account for any critical files. The "orphaned" files are either:
>
> - **Internal debris from Docker/containerd** (completely harmless),
> - **An ISO images** that was probably downloaded by a user account that no longer exists on this machine.
>   You can safely claim ownership of the ISOs with `chown` if you want, and ignore the container stuff entirely.

### `cat /etc/shadow`

Contains the encrypted password, details about the passwords.

```sh
❯ cat /etc/shadow
cat: /etc/shadow: Permission denied

❯ sudo cat /etc/shadow
root: ENCRYPTED BULLSHIT HERE
bin:!*:20627:::::
daemon:!*:20627:::::
mail:!*:20627:::::
ftp:!*:20627:::::
http:!*:20627:::::
nobody:!*:20627:::::
dbus:!*:20627::::::
mava: ENCRYPTED BULLSHIT HERE TOO
rtkit:!*:20627::::
git:!*:20627::::
nvidia-persistenced:!*:20628:::::
systemd-imds:!*:20628:::::
postgres:!*:20628::::::
valkey:!*:20628:::::
```

- The format: `username:password_hash:last_change:min:max:warn:inactive:expire:reserved`

- `!*`: means "locked and invalid"; no usable password & cannot authenticate via login

- `expire` (the `:1:` you see at the end of many lines): the day on which the account permanently expires, also counted in days since 1970.
  `1` means it expired on January 2, 1970 - so these accounts have been dead for over 50 years. (standard extra lock for system users)

- Empty fields (like `::::::`): the system uses default values (no minimum age, no maximum age, no warning, no inactivity lock); but since the password is `!*`, none of that matters anyway.

- Only `root` and `mava` have real, working passwords.

> [!WARNING] Security Tip
> Keep this file safe. Never share the actual hash strings - they're what attackers would try to crack.

## `cat /etc/group`

The system's group database; defines all the groups on your system and which users are members of each group.

```sh
❯ cat /etc/group
root:x:0:root
sys:x:3:bin
mem:x:8:
ftp:x:11:
mail:x:12:
log:x:19:
smmsp:x:25:
proc:x:26:
games:x:50:
lock:x:54:
network:x:90:
floppy:x:94:
scanner:x:96:
power:x:98:
nobody:x:65534:
adm:x:999:daemon
wheel:x:998:mava
empower:x:997:
utmp:x:996:
audio:x:995:
clock:x:994:
disk:x:993:
input:x:992:
kmem:x:991:
kvm:x:990:
lp:x:989:
optical:x:988:
render:x:987:
sgx:x:986:
storage:x:985:
tty:x:5:
uucp:x:984:
video:x:983:
users:x:982:
systemd-journal:x:981:
rfkill:x:980:
bin:x:1:daemon
daemon:x:2:bin
http:x:33:
dbus:x:81:
systemd-coredump:x:979:
systemd-network:x:978:
systemd-oom:x:977:
systemd-journal-remote:x:976:
systemd-resolve:x:975:
systemd-timesync:x:974:
tss:x:973:
uuidd:x:972:
alpm:x:971:
polkitd:x:102:
avahi:x:970:
pcscd:x:969:
mava:x:1000:
rtkit:x:968:
seat:x:967:
git:x:966:
nvidia-persistenced:x:143:
systemd-imds:x:965:
docker:x:964:mava
postgres:x:963:
valkey:x:962:
mattermost:x:961:
```

- format of each line: `group_name:password_placeholder:GID:member_list`

- `x`: the group password is stored in `/etc/gshadow` (almost always the case - group passwords are rarely used).
- `GID` = Group ID (numeric).
- `member_list` = users (comma‑separated) who have this as a **supplementary group**.

- The most important things about **YOUR** user (`mava`)

| Group    | GID  | Members   | What it means for **you**                                                                                                                                |
| :------- | :--- | :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `wheel`  | 998  | `mava`    | You are an administrator. On most distros, the `wheel` group is configured in `/etc/sudoers` to allow members to run `sudo`. So you can elevate to root. |
| `docker` | 964  | `mava`    | You can run Docker commands without `sudo`.                                                                                                              |
| `mava`   | 1000 | _(empty)_ | This is your **primary group** (set in `/etc/passwd`). Any files you create will normally belong to this group.                                          |

> [!WARNING] Security Note
> Being in `docker` gives effectively **root‑level access** to the FUCKING **HOST** (since you can mount the host filesystem into containers). Keep this in mind!

- System / Hardware access groups (standard)

These groups exist so you can be added to them if you need hardware permissions (e.g., to use audio, video, or VMs). Currently, _none_ have you listed, so they're just available.

| Group     | GID | Purpose                                                                                    |
| :-------- | :-- | :----------------------------------------------------------------------------------------- |
| `audio`   | 995 | Access to audio devices (sound cards).                                                     |
| `video`   | 983 | Access to video hardware (GPU, framebuffer).                                               |
| `render`  | 987 | GPU rendering (e.g., for Vulkan/Mesa to use the GPU for compute).                          |
| `kvm`     | 990 | Access to **KVM** (virtualization) - needed to run QEMU/KVM VMs without root.              |
| `input`   | 992 | Access to input devices (keyboard, mouse, touchpad) - often needed for games or raw input. |
| `optical` | 988 | Access to CD/DVD/Blu‑ray drives.                                                           |
| `storage` | 985 | Access to storage devices (external drives, etc.).                                         |
| `disk`    | 993 | Direct raw disk access (dangerous, but sometimes needed for low‑level tools).              |
| `lp`      | 989 | Access to parallel printers / legacy printing.                                             |
| `scanner` | 96  | Access to scanners (via SANE).                                                             |
| `power`   | 98  | For power management (suspend/reboot).                                                     |
| `network` | 90  | Network configuration access.                                                              |
| `rfkill`  | 980 | Toggle WiFi/Bluetooth radios on/off.                                                       |
| `seat`    | 967 | Seat management (used by `logind` for multi‑seat setups).                                  |

- System & service accounts (background groups)
  These are created by installed packages so their services can run with the correct permissions. No users need to be in these - they're for daemons.

| Group              | GID | Belongs to                                                                                            |
| :----------------- | :-- | :---------------------------------------------------------------------------------------------------- |
| `systemd-journal`  | 981 | Allows reading the systemd journal logs (if you add yourself, you can run `journalctl` without sudo). |
| `systemd-network`  | 978 | systemd-networkd (network management).                                                                |
| `systemd-resolve`  | 975 | systemd-resolved (DNS).                                                                               |
| `systemd-timesync` | 974 | systemd-timesyncd (time sync).                                                                        |
| `systemd-coredump` | 979 | Core dump handler.                                                                                    |
| `dbus`             | 81  | D‑Bus message bus.                                                                                    |
| `polkitd`          | 102 | PolicyKit (authorization framework).                                                                  |
| `tss`              | 973 | TPM 2.0 (Trusted Platform Module).                                                                    |
| `uuidd`            | 972 | UUID generator.                                                                                       |
| `rtkit`            | 968 | RealtimeKit (audio/process priority).                                                                 |
| `alpm`             | 971 | Arch Linux Pacman package manager (internal).                                                         |
| `empower`          | 997 | Arch‑specific group for `systemd` power management (allows suspend/shutdown without password).        |
| `utmp`             | 996 | User accounting (login records).                                                                      |

- Installed server / application groups

| Group                 | GID | Installed software                |
| :-------------------- | :-- | :-------------------------------- |
| `http`                | 33  | Web server (Apache/Nginx).        |
| `git`                 | 966 | Git daemon.                       |
| `postgres`            | 963 | PostgreSQL database.              |
| `valkey`              | 962 | Valkey (Redis‑compatible cache).  |
| `mattermost`          | 961 | Mattermost chat server.           |
| `docker`              | 964 | Docker container runtime.         |
| `nvidia-persistenced` | 143 | NVIDIA GPU persistence daemon.    |
| `avahi`               | 970 | Avahi (mDNS / network discovery). |
| `pcscd`               | 969 | Smart card daemon.                |

- Legacy / historical groups
  `bin`, `sys`, `daemon`, `games`, `lock`, `floppy`, `uucp`: these are relics from older Unix systems. Mostly sit around for compatibility with very old software.
  `adm:x:999:daemon`: the `adm` group is traditionally for system monitoring/log reading, but here it only contains the `daemon` user.

#### Quick verification: what groups is `mava` actually in?

To see all groups your user belongs to, run:

```bash
groups mava
# or
id mava
```

Based on this file, the _supplementary_ groups you're in are:

- `wheel` (sudo power)
- `docker` (container power)

Your _primary_ group is `mava` (GID 1000).

## `cat /etc/sudoers`

```sh
❯ cat /etc/sudoers
cat: /etc/sudoers: Permission denied

❯ sudo cat /etc/sudoers
## sudoers file.
##
## This file MUST be edited with the 'visudo' command as root.
## Failure to use 'visudo' may result in syntax or file permission errors
## that prevent sudo from running.
##
## See the sudoers man page for the details on how to write a sudoers file.
##

##
## Host alias specification
##
## Groups of machines. These may include host names (optionally with wildcards),
## IP addresses, network numbers or netgroups.
# Host_Alias	WEBSERVERS = www1, www2, www3

##
## User alias specification
##
## Groups of users.  These may consist of user names, uids, Unix groups,
## or netgroups.
# User_Alias	ADMINS = millert, dowdy, mikef

##
## Cmnd alias specification
##
## Groups of commands.  Often used to group related commands together.
# Cmnd_Alias	PROCESSES = /usr/bin/nice, /bin/kill, /usr/bin/renice, \
# 			    /usr/bin/pkill, /usr/bin/top
#
# Cmnd_Alias	REBOOT = /sbin/halt, /sbin/reboot, /sbin/poweroff
#
# Cmnd_Alias	DEBUGGERS = /usr/bin/gdb, /usr/bin/lldb, /usr/bin/strace, \
# 			    /usr/bin/truss, /usr/bin/bpftrace, \
# 			    /usr/bin/dtrace, /usr/bin/dtruss
#
# Cmnd_Alias	PKGMAN = /usr/bin/apt, /usr/bin/dpkg, /usr/bin/rpm, \
# 			 /usr/bin/yum, /usr/bin/dnf,  /usr/bin/zypper, \
# 			 /usr/bin/pacman

##
## Defaults specification
##
## Preserve editor environment variables for visudo.
## To preserve these for all commands, remove the "!visudo" qualifier.
Defaults!/usr/bin/visudo env_keep += "SUDO_EDITOR EDITOR VISUAL"
##
## Use a hard-coded PATH instead of the user's to find commands.
## This also helps prevent poorly written scripts from running
## arbitrary commands under sudo.
Defaults secure_path="/usr/local/sbin:/usr/local/bin:/usr/bin"
##
## You may wish to keep some of the following environment variables
## when running commands via sudo.
##
## Locale settings
# Defaults env_keep += "LANG LANGUAGE LINGUAS LC_* _XKB_CHARSET"
##
## Run X applications through sudo; HOME is used to find the
## .Xauthority file.  Note that other programs use HOME to find
## configuration files and this may lead to privilege escalation!
# Defaults env_keep += "HOME"
##
## X11 resource path settings
# Defaults env_keep += "XAPPLRESDIR XFILESEARCHPATH XUSERFILESEARCHPATH"
##
## Desktop path settings
# Defaults env_keep += "QTDIR KDEDIR"
##
## Allow sudo-run commands to inherit the callers' ConsoleKit session
# Defaults env_keep += "XDG_SESSION_COOKIE"
##
## Uncomment to enable special input methods.  Care should be taken as
## this may allow users to subvert the command being run via sudo.
# Defaults env_keep += "XMODIFIERS GTK_IM_MODULE QT_IM_MODULE QT_IM_SWITCHER"
##
## Uncomment to disable "use_pty" when running commands as root.
## Commands run as non-root users will run in a pseudo-terminal,
## not the user's own terminal, to prevent command injection.
# Defaults>root !use_pty
##
## Uncomment to run commands in the background by default.
## This can be used to prevent sudo from consuming user input while
## a non-interactive command runs if "use_pty" or I/O logging are
## enabled.  Some commands may not run properly in the background.
# Defaults exec_background
##
## Uncomment to send mail if the user does not enter the correct password.
# Defaults mail_badpass
##
## Uncomment to enable logging of a command's output, except for
## sudoreplay and reboot.  Use sudoreplay to play back logged sessions.
## Sudo will create up to 2,176,782,336 I/O logs before recycling them.
## Set maxseq to a smaller number if you don't have unlimited disk space.
# Defaults log_output
# Defaults!/usr/bin/sudoreplay !log_output
# Defaults!/usr/local/bin/sudoreplay !log_output
# Defaults!REBOOT !log_output
# Defaults maxseq = 1000
##
## Uncomment to disable intercept and log_subcmds for debuggers and
## tracers.  Otherwise, anything that uses ptrace(2) will be unable
## to run under sudo if intercept_type is set to "trace".
# Defaults!DEBUGGERS !intercept, !log_subcmds
##
## Uncomment to disable intercept and log_subcmds for package managers.
## Some package scripts run a huge number of commands, which is made
## slower by these options and also can clutter up the logs.
# Defaults!PKGMAN !intercept, !log_subcmds
##
## Uncomment to disable PAM silent mode.  Otherwise messages by PAM
## modules such as pam_faillock will not be printed.
# Defaults !pam_silent

##
## Runas alias specification
##

##
## User privilege specification
##
root ALL=(ALL:ALL) ALL

## Uncomment to allow members of group wheel to execute any command
%wheel ALL=(ALL:ALL) ALL

## Same thing without a password
# %wheel ALL=(ALL:ALL) NOPASSWD: ALL

## Uncomment to allow members of group sudo to execute any command
# %sudo ALL=(ALL:ALL) ALL

## Uncomment to allow any user to run sudo if they know the password
## of the user they are running the command as (root by default).
# Defaults targetpw  # Ask for the password of the target user
# ALL ALL=(ALL:ALL) ALL  # WARNING: only use this together with 'Defaults targetpw'

## Read drop-in files from /etc/sudoers.d
@includedir /etc/sudoers.d
```

Bottom‑line up front:

- You (`mava`) are in the `wheel` group.
- The line `%wheel ALL=(ALL:ALL) ALL` is **active** (uncommented).
  This means **you can run _any_ command as _any_ user (including root)** using `sudo`.
- You must type your own password every time (the `NOPASSWD` line is commented out).

| Line / Rule                                                        | Translation                                                                                                                                                                                                                                                                                                                    |
| :----------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Defaults!/usr/bin/visudo env_keep += "SUDO_EDITOR EDITOR VISUAL"` | When you run `sudo visudo` to edit this file, it keeps your preferred text‑editor settings (like `EDITOR=nano`).                                                                                                                                                                                                               |
| `Defaults secure_path="/usr/local/sbin:/usr/local/bin:/usr/bin"`   | **Security feature.** When you run a command with `sudo`, it ignores your personal `PATH` and uses this strict, safe list of system folders. This prevents hackers from sneaking in a fake `ls` or `cat` command that could steal your password.                                                                               |
| `root ALL=(ALL:ALL) ALL`                                           | The **root** user can run any command on any machine, as any user, in any group – total power (obviously).                                                                                                                                                                                                                     |
| `%wheel ALL=(ALL:ALL) ALL`                                         | **This is the one that applies to you.**<br>• `%wheel` = any user in the **`wheel`** group (that's you!).<br>• `ALL=(ALL:ALL)` = on any host, **as any user** (e.g., `sudo -u postgres`), **and any group**.<br>• `ALL` = run **any command**.<br>**Result:** You have full admin rights, but you need to enter your password. |
| `@includedir /etc/sudoers.d`                                       | Sudo will also load any extra rule files placed inside `/etc/sudoers.d/`. (This folder is probably empty, but it's standard for packages to drop rules there without touching the main file).                                                                                                                                  |

| Commented Line                         | What it would mean if uncommented                                                                                                                                                        |
| :------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `# %wheel ALL=(ALL:ALL) NOPASSWD: ALL` | If this were active, members of `wheel` (including you) could run `sudo` **without ever typing a password**. It is **off**, so you _must_ type your password.                            |
| `# %sudo ALL=(ALL:ALL) ALL`            | This would give admin rights to a group called `sudo` (like on Ubuntu/Debian). On your Arch system, that group doesn't exist (we saw no `sudo` group in `/etc/group`), so it's disabled. |
| `# Defaults targetpw`                  | This would force you to type the _target user's_ password (e.g., root's password) instead of your own. It's off, so you use your own password.                                           |

### Summary of what this means for **you** as `mava`

1. You are a full system administrator.
   You can do absolutely anything: install packages, delete system files, change ownership, restart services, etc.

2. You must authenticate every time.
   When you run `sudo <command>`, it asks for **your** password (not root's); it remembers it for a short time, usually ~5 minutes

3. Your commands run in a safe environment.
   Even if you set a weird `PATH` in your `.zshrc`, `sudo` ignores it and uses the secure system paths to find binaries – protecting you from accidentally running a malicious script.

4. One quick security note (since you're in `wheel`)
   Any command you run with `sudo` can potentially break your system or delete your files.
   Also, since `docker` group membership (we saw earlier) is effectively root access, the fact that you have both `wheel` and `docker` rights means you are **fully privileged**. This is fine for a personal desktop or dev machine.

## `lastlog`

```sh
❯ lastlog
zsh: command not found: lastlog

❯ lastlog2
Username         Port     From                                       Latest
mava             tty1                                                Sat Jul 25 04:04:22 +0330 2026
root             tty1                                                Wed Jun 24 02:59:28 +0330 2026
```

This is the output of `lastlog2`– a tool that shows you the most recent login time for every user on your system.
(Your system doesn’t have the older`lastlog`, but `lastlog2` does the same job, just newer.)

- The Output Table

| Username   | Port / Terminal | From (Source IP)  | Latest Login Time                  |
| :--------- | :-------------- | :---------------- | :--------------------------------- |
| **`mava`** | `tty1`          | _(blank – local)_ | **Sat Jul 25 04:04:22 +0330 2026** |
| **`root`** | `tty1`          | _(blank – local)_ | **Wed Jun 24 02:59:28 +0330 2026** |

- Username`: The account that logged in.
- Port`/`tty`: The terminal/device used:
  - `tty1` = the physical/local console (the monitor/keyboard directly plugged into your machine). Not SSH, not a remote session.
- `From`: The remote IP address if the login came over the network (SSH, etc.). Since this is blank, both logins were local (you sat down at the machine and logged in).
- `Latest`: The exact timestamp of the last login

> Why don't we see any other users?
> All those other users from `/etc/passwd` – `bin`, `daemon`, `http`, `postgres`, `mattermost`, etc. – do not appear in this list.  
> Why? Because they have never logged in interactively. They are **system/service accounts** with shells like `/usr/bin/nologin`. They only run background processes; no human has ever typed a password for them at a login prompt. `lastlog2` only tracks actual login sessions, so they simply don't have a record.

## `tail auth.log`

```sh
❯ sudo grep -rn "auth.log" /var/log/*
grep: /var/log/journal/fe290c67e7bc4cafbadd8ccd3ccebd07/user-1000.journal: binary file matches
```

On Arch Linux (your system), there is NO plain-text /var/log/auth.log file.

That file exists on Debian/Ubuntu systems. On Arch, all authentication logs are stored inside the systemd journal – not in separate plain-text files.

- How to actually **check authentication logs** on your system

Since you're on Arch with `systemd`, use `journalctl` instead of grepping plain files.

| What you want to see                                     | Command                                                                           |
| :------------------------------------------------------- | :-------------------------------------------------------------------------------- |
| All authentication-related logs (sudo, logins, SSH, PAM) | `sudo journalctl -g "authentication\|pam\|sudo\|login" -b`                        |
| Just sudo commands run by users                          | `sudo journalctl -g "sudo" -b`                                                    |
| Login attempts (local/SSH)                               | `sudo journalctl -g "session opened\|login" -b`                                   |
| Failed password attempts                                 | `sudo journalctl -g "Failed password"`                                            |
| All logs from today (then filter)                        | `sudo journalctl -b -0` (current boot) or `sudo journalctl -b -1` (previous boot) |

> Add `-f` at the end to "follow" and watch real-time, like `tail -f`.

```sh
# All authentication events from this boot
sudo journalctl -g "pam|sudo|sshd|login" -b

# Just sudo commands (with details)
sudo journalctl -g "sudo" -b

# Failed login attempts (if any)
sudo journalctl -g "Failed password" -b

# See all logs from today and follow (like tail -f)
sudo journalctl -b -f
```

## `history | less`

```sh
 1441  sudo find / -nouser -print
 1447  cat /etc/shadow
 1448  sudo cat /etc/shadow
 1450  cat /etc/group
 1452  cat /etc/sudoers
 1453  sudo cat /etc/sudoers
 1455  lastlog
 1456  lastlog2
 1458  tail auth.log
 1460  cleasr
 1462  grep "auth.log" /var/log
 1463  grep "auth.log" /var/log/
 1464  grep "auth.log" /var/log/*
 1465  sudo grep "auth.log" /var/log/*
 1466  sudo grep -rn "auth.log" /var/log/*
 1467  clear
(END)
```

## `uptime`

```sh
❯ uptime
 00:40:18 up 3 days, 20:36,  1 user,  load average: 1.02, 0.81, 0.75
```

The format: `current_time up up_time, users_logged_in, load average on CPU: over_last_1min, over_last_5min, over_last_15min`

> [!NOTE] What do the load averages actually mean for _your_ system?
> 1.00: CPU is 100% busy on a **single‑core** machine.
> On **multi‑core** machines divide the load by the number of CPU cores to get the real utilization percentage.
>
> - If you have a 4‑core CPU, a load of `1.02` means it's only using **~25%** of your total processing power. If you have an 8‑core CPU, it's even less.
>
> The trend tells a story:
>
> - `1.02` (1 min) → `0.81` (5 min) → `0.75` (15 min)
>   Your load is decreasing. It was slightly busier a short while ago (maybe you just finished compiling something, ran a heavy script, or opened a large app), and now it's calming down to its normal baseline of ~0.75. This is **perfectly healthy** – nothing is spiking out of control.

## `free`

```sh
❯ free
               total        used        free      shared  buff/cache   available
Mem:        16233212     5236212      890284      678072    11125260    10997000
Swap:        4194300      720676     3473624
```

`free` output shows you how your system's **RAM (memory) and Swap (disk‑based "emergency" memory)** are being used. (All in kilobytes)

| Column         | Value (KB) | Value (approx. GB) | What it actually means                                                                                                                                                                                                                         |
| :------------- | :--------- | :----------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| total          | 16,233,212 | ~15.5 GB           | 16 GB of physical RAM installed.                                                                                                                                                                                                               |
| used           | 5,236,212  | ~5.0 GB            | Running programs and system processes are actively using 5 GB right now.                                                                                                                                                                       |
| free           | 890,284    | ~0.85 GB           | Only 850 MB is completely empty and not used for _anything_ at this exact moment. (This looks low, but don't panic – see the next column!)                                                                                                     |
| shared         | 678,072    | ~0.65 GB           | Memory shared between multiple processes (usually tmpfs filesystems like `/dev/shm` or shared libraries).                                                                                                                                      |
| **buff/cache** | 11,125,260 | ~10.6 GB           | **This is the secret.** Linux has loaded 10.6 GB of file data into RAM as a **cache**. This speeds up your system enormously (faster app launches, faster file reads). This cache is automatically freed whenever your programs need more RAM. |
| **available**  | 10,997,000 | ~10.5 GB           | THIS IS REAL FREE MEMORY. This is the amount of RAM you can immediately use for new applications _without_ hitting swap. You have 10.5 GB ready to go – that's plenty!                                                                         |

> [!NOTE]
> Even though `free` (the column) shows only 0.85 GB empty, you effectively have 10.5 GB free because Linux happily sacrifices that cache when you actually need it.

### The breakdown of **Swap** (disk space used as slow "overflow" memory)

| Column | Value (KB) | Value (approx. GB) | What it actually means                             |
| :----- | :--------- | :----------------- | :------------------------------------------------- |
| total  | 4,194,300  | ~4.0 GB            | **4 GB swap partition** or swap file set up.       |
| used   | 720,676    | ~0.7 GB            | **720 MB** of swap is currently in use.            |
| free   | 3,473,624  | ~3.3 GB            | **3.3 GB** of swap still available if you need it. |

> [!NOTE] Why is **720 MB of swap** being used when I have 10.5 GB of free RAM?
> The Linux kernel has a tendency to **swap out inactive background processes** to disk when it decides they haven't been touched in a while. This frees up physical RAM to be used for **disk caching** (that huge 10.6 GB buffer/cache), which makes the overall system feel snappier.

Since your `available` RAM is still over 10 GB, the 720 MB of swap usage is **NOT a sign of memory pressure**. It just means some old background daemons (or maybe a forgotten browser tab or Docker container) have been pushed to swap because they're idle. If you actually run out of RAM, the kernel will pull them back from swap automatically.

NOTE: If you were constantly hitting 90–100% swap usage _&_`available` was near zero, _then_ you'd have a problem.

---

---

---

---

---

---

file:///home/mava/Downloads/daneshkar/Linux%20Incident%20Response%20Cheat%20Sheet.pdf

PAGE 9, END OF `FREE`
