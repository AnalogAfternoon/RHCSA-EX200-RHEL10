# Lesson 15 — Working with Systemd

> 📺 *Video coming soon!*

---

## Overview

Systemd is the init system and service manager used in RHEL. It controls how services start, stop, and depend on each other. Understanding systemd is essential for any Linux administrator.

---

## Subtopics

- 15.1 Understanding the Role of Systemd
- 15.2 Exploring Systemd Units
- 15.3 Managing Systemd Services
- 15.4 Modifying Systemd Unit Configuration
- 15.5 Managing Unit Dependencies
- 15.6 Masking Services
- 15.7 Using Systemd to Run Anything

---

## Systemd Unit Types

| Unit Type | Extension | Purpose |
|-----------|-----------|---------|
| Service | `.service` | Manages daemons and background processes |
| Socket | `.socket` | Manages IPC sockets |
| Timer | `.timer` | Schedules tasks (like cron) |
| Mount | `.mount` | Manages filesystem mount points |
| Target | `.target` | Groups units — similar to runlevels |

---

## Managing Services

| Command | Description |
|--------|-------------|
| `systemctl start service` | Start a service immediately |
| `systemctl stop service` | Stop a service immediately |
| `systemctl restart service` | Stop and start a service |
| `systemctl reload service` | Reload config without restarting |
| `systemctl status service` | Show current status of a service |
| `systemctl enable service` | Enable service to start at boot |
| `systemctl disable service` | Disable service from starting at boot |
| `systemctl is-active service` | Check if a service is currently running |
| `systemctl is-enabled service` | Check if a service is enabled at boot |

## Listing and Viewing Units

| Command | Description |
|--------|-------------|
| `systemctl list-units` | List all active units |
| `systemctl list-units --type=service` | List only active services |
| `systemctl list-unit-files` | List all installed unit files and their state |
| `systemctl cat service` | View the unit file for a service |
| `systemctl show service` | Show all properties of a unit |

## Unit Dependencies

| Command | Description |
|--------|-------------|
| `systemctl list-dependencies service` | Show what a unit depends on |
| `systemctl list-dependencies --reverse service` | Show what depends on this unit |

## Masking Services

Masking is stronger than disabling — it prevents a service from being started at all, even manually.

| Command | Description |
|--------|-------------|
| `systemctl mask service` | Mask a service — completely prevents it from starting |
| `systemctl unmask service` | Remove the mask from a service |

## Modifying Unit Configuration

| Command | Description |
|--------|-------------|
| `systemctl edit service` | Edit a unit file override (creates drop-in file) |
| `systemctl daemon-reload` | Reload systemd after making changes to unit files |

---

## Examples

```bash
systemctl start sshd
# Starts the SSH daemon right now

systemctl enable sshd
# Makes SSH start automatically at every boot

systemctl status firewalld
# Shows whether the firewall is running, recent logs, PID

systemctl list-units --type=service
# Lists all currently active services

systemctl cat sshd.service
# Shows the full sshd unit file

systemctl mask bluetooth
# Completely prevents bluetooth from starting

systemctl daemon-reload
# Required after editing any unit file
```

---

## Key Takeaway

Systemd management is a core RHCSA topic. Know `start`, `stop`, `restart`, `enable`, `disable`, and `status` cold. Understand the difference between **stopping** (temporary) and **disabling** (survives reboot), and between **disabling** and **masking** (masking is absolute). Always run `daemon-reload` after editing unit files.
