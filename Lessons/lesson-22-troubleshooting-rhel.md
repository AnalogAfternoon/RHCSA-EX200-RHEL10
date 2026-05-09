# Lesson 22 — Troubleshooting RHEL

## Overview

Troubleshooting is one of the most important skills for any system administrator. This lesson covers how to boot into recovery modes, reset a lost root password, and fix common system issues that prevent normal boot.


## Subtopics

- 22.1 Using Troubleshooting Modes
- 22.2 Recovering a Lost Root User Password
- 22.3 Using the Boot Debug Shell
- 22.4 Troubleshooting Filesystem Issues
- 22.5 Fixing Network Issues
- 22.6 Managing Performance Issues
- 22.7 Troubleshooting Software Issues
- 22.8 Fixing Memory Shortage
- 22.9 Using sos report
- 22.10 Consulting Red Hat Website for Tips

## Troubleshooting Modes

When a system won't boot normally, you can interrupt the boot process and enter a special mode for repairs.

### Rescue Mode

A minimal environment with most filesystems mounted. Good for fixing configuration issues.

```
At GRUB menu → press e → find linux line → append:
systemd.unit=rescue.target
→ Ctrl+X to boot
```

### Emergency Mode

Even more minimal than rescue — only the root filesystem is mounted read-only. Used when rescue mode won't start.

```
At GRUB menu → press e → find linux line → append:
systemd.unit=emergency.target
→ Ctrl+X to boot
```

### rd.break — Early Boot Shell

Drops you into a shell before the root filesystem is fully mounted. Required for password recovery.

```
At GRUB menu → press e → find linux line → append:
rd.break
→ Ctrl+X to boot
```

## Recovering a Lost Root Password

This is a step-by-step procedure — follow it exactly.

### Step 1 — Interrupt the Boot at GRUB

- Restart the system
- At the GRUB menu, press **e** to edit
- Find the line starting with `linux`
- At the end of that line, add: `rd.break`
- Press **Ctrl+X** to boot

### Step 2 — Remount the Root Filesystem as Read-Write

```bash
mount -o remount,rw /sysroot
```

### Step 3 — Enter the Installed System (chroot)

```bash
chroot /sysroot
```

### Step 4 — Reset the Root Password

```bash
passwd root
# Enter and confirm the new password
```

### Step 5 — Relabel SELinux

```bash
touch /.autorelabel
# Required so SELinux accepts the changed password file
```

### Step 6 — Exit and Reboot

```bash
exit
exit
# System will reboot and SELinux relabeling will run automatically
```

## Other Common Troubleshooting Commands

| Command | Description |
|--------|-------------|
| `journalctl -b -p err` | Show all errors from the current boot |
| `journalctl -xb` | Show boot logs with explanations |
| `systemctl --failed` | List all units that failed to start |
| `systemctl status unit` | Check status and recent logs for a unit |
| `dmesg` | Show kernel ring buffer messages (hardware, boot) |
| `dmesg | grep error` | Filter kernel messages for errors |
| `fsck /dev/sdb1` | Check and repair a filesystem |

## Key Takeaway

Root password recovery using `rd.break` is a common RHCSA exam task — practice it until you can do it from memory. Know the difference between rescue, emergency, and rd.break modes. Always remember to `touch /.autorelabel` after making changes in chroot, or SELinux will block the login. `systemctl --failed` is the fastest way to spot what went wrong after a bad boot.
