---

## Package Manager

### Installing Packages

```bash
# Install package from official repositories
sudo pacman -S [package]

# Install package from AUR
yay -S [package]

# Install multiple packages
sudo pacman -S [package1] [package2] [package3]

# Install package without confirmation prompts
sudo pacman -S --noconfirm [package]
```

### Updating System

```bash
# Update package database and upgrade all packages
sudo pacman -Syu

# Update AUR packages and system packages
yay -Syu

# Force refresh package database before updating
sudo pacman -Syyu
```

### Removing Packages

```bash
# Remove package only
sudo pacman -R [package]

# Remove package with its dependencies (not required by other packages)
sudo pacman -Rs [package]

# Remove package, dependencies, and configuration files
sudo pacman -Rns [package]

# Remove orphaned packages (no longer required by any installed package)
sudo pacman -Rns $(pacman -Qtdq)
```

### Searching Packages

```bash
# Search in official repositories
pacman -Ss [keyword]

# Search in AUR
yay -Ss [keyword]

# Search only in installed packages
pacman -Qs [keyword]
```

### Package Information

```bash
# Show detailed information about a package
pacman -Si [package]        # from repository
pacman -Qi [package]        # if installed
yay -Si [package]           # from AUR

# List files installed by a package
pacman -Ql [package]

# Find which package owns a file
pacman -Qo /path/to/file

# List explicitly installed packages
pacman -Qe

# List packages that need to update
pacman -Qu
yay -Qu
```

### Listing Packages

```bash
# List all installed packages
pacman -Q
yay -Q

# List explicitly installed packages (not dependencies)
pacman -Qe

# List packages installed from AUR
pacman -Qm

# List packages from official repositories
pacman -Qn

# List orphaned packages
pacman -Qtd
```

### Cleaning Cache

```bash
# Remove all cached packages (not installed)
sudo pacman -Sc

# Remove all cached packages (including installed)
sudo pacman -Scc

# Clean AUR cache
yay -Sc
yay -Scc

# Remove only uninstalled package cache (safer)
sudo paccache -r

# Keep only the last 3 versions of cached packages
sudo paccache -rk3
```

### Common Flags

| Flag | Description |
|------|-------------|
| `-S` | Sync/install packages |
| `-R` | Remove packages |
| `-Q` | Query installed packages |
| `-s` | Search for packages |
| `-u` | Upgrade packages |
| `-y` | Refresh package database |
| `-c` | Clean cache |
| `-i` | Show information |
| `-l` | List files |
| `-o` | Query file owner |
| `--noconfirm` | Skip confirmation prompts |

---

## Audio Control (PipeWire)

### Managing Application Audio

```bash
# List all audio sinks/streams
wpctl status

# Mute a specific application by ID
wpctl set-mute [ID] 1

# Unmute a specific application by ID
wpctl set-mute [ID] 0

# Toggle mute for a specific application
wpctl set-mute [ID] toggle

# Set volume for a specific application (0.0 to 1.0)
wpctl set-volume [ID] 0.5

# Increase volume by 5%
wpctl set-volume [ID] 5%+

# Decrease volume by 5%
wpctl set-volume [ID] 5%-
```

---

## Disk Management

### Formatting and Mounting Secondary Drives

#### Identify the Drive

```bash
# List all block devices
lsblk

# Show detailed disk information
sudo fdisk -l

# Display partition information
sudo blkid
```

#### Format the Drive

```bash
# Create a new partition table (WARNING: destroys all data)
sudo fdisk /dev/sdX

# Format partition as ext4
sudo mkfs.ext4 /dev/sdX1

# Format partition as NTFS (requires ntfs-3g package)
sudo mkfs.ntfs /dev/sdX1

# Format partition as exFAT (requires exfatprogs package)
sudo mkfs.exfat /dev/sdX1

# Format entire disk as ext4 (without partition table)
sudo mkfs.ext4 /dev/sdX
```

#### Mount the Drive

```bash
# Create mount point
sudo mkdir -p /mnt/data

# Mount temporarily
sudo mount /dev/sdX1 /mnt/data

# Unmount
sudo umount /mnt/data
```

#### Permanent Mount (via /etc/fstab)

```bash
# Get UUID of the partition
sudo blkid /dev/sdX1

# Edit fstab
sudo vim /etc/fstab

# Add entry (replace UUID with actual UUID from blkid)
UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx /mnt/data ext4 defaults 0 2

# Test fstab configuration
sudo mount -a

# Verify mount
df -h
```

#### Common fstab Options

| Option | Description |
|--------|-------------|
| `defaults` | Use default mount options (rw, suid, dev, exec, auto, nouser, async) |
| `noatime` | Don't update access time (improves performance) |
| `nofail` | Don't fail boot if device is missing |
| `auto` | Mount automatically at boot |
| `noauto` | Don't mount automatically (mount manually) |
| `user` | Allow regular users to mount |
| `0` | Dump field (0 = no backup) |
| `2` | fsck order (0 = no check, 1 = root, 2 = other) |

#### Set Permissions

```bash
# Change ownership to current user
sudo chown -R $USER:$USER /mnt/data

# Set permissions (read, write, execute for owner)
sudo chmod 755 /mnt/data
```

#### Important Notes

- **lost+found folder**: After formatting with ext4, a `lost+found` directory will appear at the root of the partition. This is used by the filesystem for recovery purposes. Do not delete or modify it.

---

## Account Management

### Account Lockout (pam_faillock)

#### Unlock a Locked Account

```bash
# Unlock specific user account
sudo faillock --user [username] --reset

# View failed login attempts for a user
sudo faillock --user [username]

# View all locked accounts
sudo faillock
```

#### Configure Faillock Settings

Edit the PAM configuration file:

```bash
sudo vim /etc/security/faillock.conf
```

Common configuration options:

```conf
# Number of failed attempts before lockout (default: 3)
deny = 5

# Lockout duration in seconds (default: 600 = 10 minutes)
# Set to 0 for permanent lockout until manual reset
unlock_time = 300

# Time window for counting failed attempts (default: 900 = 15 minutes)
fail_interval = 900

# Allow root account to be locked (default: no)
even_deny_root

# Root account lockout duration (default: 600)
root_unlock_time = 600
```

#### Apply Configuration Changes

After editing `/etc/security/faillock.conf`, the changes take effect immediately. No service restart required.

#### Check PAM Configuration

```bash
# View PAM configuration for system-auth
cat /etc/pam.d/system-auth

# Verify faillock is enabled (should see pam_faillock.so entries)
grep faillock /etc/pam.d/system-auth
```

---

## Waybar

### Portal & PermissionStore Timeout Issues

#### Problem Summary

Waybar fails to start with timeout errors when attempting to communicate with xdg-desktop-portal services. This affects Waybar modules that depend on portal functionality (media controls, notifications, brightness).

#### Error Messages

```bash
(waybar:664734): dbind-WARNING **: AT-SPI: Error retrieving accessibility bus address
[error] Error calling StartServiceByName for org.freedesktop.portal.Desktop: Timeout was reached
```

**Error Analysis:**
- `dbind-WARNING / AT-SPI` - Accessibility bus warning (harmless unless accessibility features are needed)
- `Timeout calling org.freedesktop.portal.Desktop` - Waybar cannot communicate with xdg-desktop-portal backend

#### Services Involved

| Service | Description |
|---------|-------------|
| `xdg-desktop-portal` | Main portal service (DBus-activatable) |
| `xdg-desktop-portal-hyprland` | Hyprland-specific backend implementation |
| `org.freedesktop.impl.portal.PermissionStore` | DBus service for portal permissions (auto-activated) |
| `dbus` | Inter-process communication bus |

#### Debugging Process

1. **Verify portal service status**
   ```bash
   systemctl --user status xdg-desktop-portal
   systemctl --user status xdg-desktop-portal-hyprland
   ```
   Check if services are active, crashed, or failed to start.

2. **Attempt portal service restart**
   ```bash
   systemctl --user restart xdg-desktop-portal xdg-desktop-portal-hyprland
   ```
   Often resolves temporary issues, but may not fix persistent timeouts.

3. **Verify DBus activatable services**
   ```bash
   busctl --user status org.freedesktop.impl.portal.PermissionStore
   ```
   Confirms the service is activatable but may not be running.

4. **Test DBus communication**
   ```bash
   gdbus introspect --session --dest org.freedesktop.portal.Desktop --object-path /org/freedesktop/portal/desktop
   ```
   If this hangs or times out, the backend is not responsive.

5. **Restart user DBus session** (Critical step)
   ```bash
   systemctl --user restart dbus
   ```
   Clears stuck DBus connections that prevent portal activation.

6. **Restart portal services again**
   ```bash
   systemctl --user restart xdg-desktop-portal xdg-desktop-portal-hyprland
   ```
   Backend and PermissionStore should now activate correctly.

7. **Restart Waybar**
   ```bash
   pkill waybar
   waybar &
   ```
   Waybar should start without timeout errors.

#### Resolution

The root cause is typically **stuck DBus session connections** that prevent portal services from activating properly. Restarting the DBus user session resolves the blockage.

#### Key Takeaways

- `org.freedesktop.impl.portal.PermissionStore` is **DBus-activatable** - do not attempt to start it manually
- DBus session issues can block all activatable services; restarting the DBus session (`systemctl --user restart dbus`) often resolves stubborn portal timeouts
- Waybar modules relying on portals (media, notifications, brightness) will fail silently if the backend is unreachable
- The `dbind-WARNING` about AT-SPI is harmless and can be ignored unless accessibility features are required
- After system updates or session crashes, the DBus session may need to be restarted to restore portal functionality
