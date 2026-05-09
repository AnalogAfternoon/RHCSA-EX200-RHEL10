# Lesson 16 — Scheduling Tasks

## Overview

Automating tasks on a schedule is a core sysadmin skill. RHEL offers multiple scheduling tools — systemd timers for modern service-based scheduling, cron for traditional recurring jobs, and `at` for one-time future tasks.

## Subtopics

- 16.1 Exploring RHEL Scheduling Options
- 16.2 Scheduling Tasks with Systemd Timers
- 16.3 Scheduling Tasks with cron
- 16.4 Using at
- 16.5 Managing Temporary Files

## Systemd Timers

Systemd timers are the modern replacement for cron. Each timer is paired with a `.service` unit file.

| Command | Description |
|--------|-------------|
| `systemctl list-timers` | List all active timers |
| `systemctl enable --now timer-name.timer` | Enable and start a timer |
| `systemctl status timer-name.timer` | Check the status of a timer |

### Timer Unit File Example

```ini
[Unit]
Description=My Scheduled Task

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```

## cron — Traditional Scheduling

| Command | Description |
|--------|-------------|
| `crontab -e` | Edit the current user's crontab |
| `crontab -l` | List the current user's crontab entries |
| `crontab -r` | Remove the current user's crontab |
| `crontab -u user -e` | Edit another user's crontab (as root) |

### Crontab Syntax

```
* * * * * command
| | | | |
| | | | +-- Day of week (0-7, Sun=0 or 7)
| | | +---- Month (1-12)
| | +------ Day of month (1-31)
| +-------- Hour (0-23)
+---------- Minute (0-59)
```

### Crontab Examples

```bash
0 2 * * * /scripts/backup.sh
# Runs backup.sh every day at 2:00 AM

*/15 * * * * /scripts/check.sh
# Runs every 15 minutes

0 9 * * 1 /scripts/weekly.sh
# Runs every Monday at 9:00 AM
```

### System-wide cron Directories

| Directory | Schedule |
|-----------|----------|
| `/etc/cron.hourly/` | Scripts run every hour |
| `/etc/cron.daily/` | Scripts run every day |
| `/etc/cron.weekly/` | Scripts run every week |
| `/etc/cron.monthly/` | Scripts run every month |


## at — One-Time Scheduling

| Command | Description |
|--------|-------------|
| `at time` | Schedule a one-time job at a specific time |
| `atq` | List pending at jobs |
| `atrm job#` | Remove a pending at job |

```bash
at 3:00 PM
# Opens a prompt — type your command, then Ctrl+D to save

echo "dnf update -y" | at midnight
# Schedules a system update at midnight
```

## Managing Temporary Files

| Command | Description |
|--------|-------------|
| `systemd-tmpfiles --create` | Create temp files as defined in config |
| `systemd-tmpfiles --clean` | Clean up old temp files |

Config files are stored in `/etc/tmpfiles.d/` and `/usr/lib/tmpfiles.d/`.

## Key Takeaway

For the RHCSA, know both `cron` and `at`. Understand crontab syntax — the five time fields are a common exam topic. Know that systemd timers are the modern alternative to cron. Use `at` for one-off jobs and cron for repeating schedules.
