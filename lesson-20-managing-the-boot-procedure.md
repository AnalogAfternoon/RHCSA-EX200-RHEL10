# Lesson 20 — Managing the Boot Procedure

> 📺 *Video coming soon!*

---

## Overview

Understanding how Linux boots is critical for troubleshooting and system recovery. This lesson covers the RHEL boot process, how to modify GRUB2 boot parameters, and how to use systemd targets to control what the system boots into.

---

## Subtopics

- 20.1 Exploring the Boot Procedure
- 20.2 Modifying Grub2 Runtime Parameters
- 20.3 Changing Grub2 Persistent Parameters
- 20.4 Managing Systemd Targets
- 20.5 Setting the Default Systemd Target
- 20.6 Booting into a Specific Target

---

## The Boot Process (Overview)

```
BIOS/UEFI → GRUB2 Bootloader → Linux Kernel → initramfs → systemd → Default Target
```

---

## GRUB2 — Bootloader

### Runtime Changes (temporary — this boot only)

1. At the GRUB menu, press **e** to edit the boot entry
2. Find the line starting with `linux`
3. Add your parameter at the end (e.g. `rd.break` or `systemd.unit=rescue.target`)
4. Press **Ctrl+X** to boot with the changes

### Persistent Changes (survive reboots)

| File | Description |
|------|-------------|
| `/etc/default/grub` | Main GRUB2 configuration file |
| `/etc/grub.d/` | Scripts that build the final GRUB config |

```bash
# Edit the config
vim /etc/default/grub

# After making changes, rebuild the GRUB config:
grub2-mkconfig -o /boot/grub2/grub.cfg

# On UEFI systems:
grub2-mkconfig -o /boot/efi/EFI/redhat/grub.cfg
```

---

## Systemd Targets

Targets are groups of units that define what the system should be running. They replace the old SysV runlevels.

| Target | Old Runlevel | Description |
|--------|-------------|-------------|
| `poweroff.target` | 0 | Shut down the system |
| `rescue.target` | 1 | Single user / rescue mode |
| `multi-user.target` | 3 | Multi-user, no GUI (server default) |
| `graphical.target` | 5 | Multi-user with GUI |
| `reboot.target` | 6 | Reboot the system |
| `emergency.target` | — | Minimal emergency shell |

---

## Managing Targets

| Command | Description |
|--------|-------------|
| `systemctl get-default` | Show the current default target |
| `systemctl set-default target` | Set the default boot target |
| `systemctl isolate target` | Switch to a different target immediately |
| `systemctl list-units --type=target` | List all active targets |

---

## Examples

```bash
systemctl get-default
# Output: multi-user.target

systemctl set-default graphical.target
# Changes boot target to GUI on next reboot

systemctl isolate rescue.target
# Switches to rescue mode immediately (drops non-essential services)

systemctl isolate multi-user.target
# Returns to normal multi-user mode
```

### Booting into a Specific Target

At the GRUB menu, press **e**, find the `linux` line, and append:

```
systemd.unit=rescue.target
```
or
```
systemd.unit=emergency.target
```

Then press **Ctrl+X** to boot.

---

## Key Takeaway

For the RHCSA, know the boot sequence and how to interrupt it at GRUB. Know `multi-user.target` vs `graphical.target` and how to set the default with `systemctl set-default`. Booting into `rescue.target` or `emergency.target` for system recovery is a critical exam skill.
