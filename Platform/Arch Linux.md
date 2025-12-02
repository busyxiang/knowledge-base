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