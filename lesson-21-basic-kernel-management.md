# Lesson 21 — Basic Kernel Management

> 📺 *Video coming soon!*

---

## Overview

The kernel is the core of the Linux operating system. This lesson covers how to inspect the kernel, manage kernel modules, use the /proc filesystem, and make persistent kernel parameter changes.

---

## Subtopics

- 21.1 Understanding the Kernel
- 21.2 Managing Kernel Modules
- 21.3 Exploring the /proc Filesystem
- 21.4 Making Persistent Changes to /proc
- 21.5 Updating the Kernel

---

## Kernel Information

| Command | Description |
|--------|-------------|
| `uname -r` | Show the current kernel version |
| `uname -a` | Show all kernel and system info |
| `ls /boot` | List all installed kernel files |

---

## Kernel Modules

Modules are pieces of code that can be loaded into the kernel on demand — drivers, filesystems, and features are often modules.

| Command | Description |
|--------|-------------|
| `lsmod` | List all currently loaded modules |
| `modinfo module` | Show information about a module |
| `modprobe module` | Load a module into the kernel |
| `modprobe -r module` | Remove a module from the kernel |
| `rmmod module` | Remove a module (no dependency handling) |

### Making Module Loading Persistent

Create a file in `/etc/modules-load.d/`:

```bash
echo "module_name" > /etc/modules-load.d/module_name.conf
# Module will load automatically at boot
```

### Blacklisting a Module

To prevent a module from loading:

```bash
echo "blacklist module_name" > /etc/modprobe.d/blacklist.conf
```

---

## The /proc Filesystem

`/proc` is a virtual filesystem — it does not exist on disk. It exposes kernel and process information as readable files.

| Path | Description |
|------|-------------|
| `/proc/cpuinfo` | CPU information |
| `/proc/meminfo` | Memory information |
| `/proc/version` | Kernel version string |
| `/proc/loadavg` | System load averages |
| `/proc/sys/` | Kernel parameters — can be read and written |

```bash
cat /proc/cpuinfo
# Shows CPU details

cat /proc/sys/net/ipv4/ip_forward
# Shows whether IP forwarding is enabled (0=off, 1=on)

echo 1 > /proc/sys/net/ipv4/ip_forward
# Enables IP forwarding immediately (not persistent)
```

---

## sysctl — Managing Kernel Parameters

| Command | Description |
|--------|-------------|
| `sysctl -a` | List all kernel parameters |
| `sysctl parameter.name` | Show a specific parameter value |
| `sysctl -w parameter.name=value` | Set a parameter temporarily |

### Making Parameters Persistent

Add entries to `/etc/sysctl.conf` or a file in `/etc/sysctl.d/`:

```bash
# Example — enable IP forwarding persistently
echo "net.ipv4.ip_forward = 1" >> /etc/sysctl.conf

# Apply without rebooting:
sysctl -p
```

---

## Updating the Kernel

```bash
dnf update kernel
# Downloads and installs the latest kernel

# After reboot, the new kernel is used by default
# Old kernels are kept for fallback — listed in GRUB menu

dnf list installed kernel
# Shows all installed kernel versions
```

---

## Key Takeaway

For the RHCSA, know `lsmod`, `modprobe`, and `modprobe -r` for kernel modules. Understand that `/proc/sys` exposes live kernel parameters and that `sysctl -w` changes them temporarily while `/etc/sysctl.conf` makes them permanent. Always run `sysctl -p` after editing the config file to apply changes without rebooting.
