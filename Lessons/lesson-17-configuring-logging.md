# Lesson 17 — Configuring Logging

## Overview

Logging is how Linux records what is happening on the system. RHEL uses two main logging systems — `systemd-journald` for in-memory/persistent journal logs, and `rsyslogd` for traditional text-based log files. Knowing how to read and manage logs is essential for troubleshooting.


## Subtopics

- 17.1 Exploring RHEL Logging Options
- 17.2 Using systemd-journald
- 17.3 Preserving the Systemd Journal
- 17.4 Understanding rsyslogd
- 17.5 Using logrotate

## systemd-journald

| Command | Description |
|--------|-------------|
| `journalctl` | View all journal logs |
| `journalctl -u service` | View logs for a specific service |
| `journalctl -f` | Follow live log output (like tail -f) |
| `journalctl -b` | Show logs from the current boot |
| `journalctl -b -1` | Show logs from the previous boot |
| `journalctl --since "1 hour ago"` | Show logs from the last hour |
| `journalctl --since "2024-01-01" --until "2024-01-02"` | Show logs in a date range |
| `journalctl -p err` | Show only error-level messages |
| `journalctl -x` | Show logs with explanations |

### Priority Levels

| Level | Meaning |
|-------|---------|
| 0 | emerg — system is unusable |
| 1 | alert — immediate action required |
| 2 | crit — critical condition |
| 3 | err — error condition |
| 4 | warning — warning condition |
| 5 | notice — normal but significant |
| 6 | info — informational |
| 7 | debug — debug-level messages |


## Preserving the Journal

By default the journal is stored in memory and lost on reboot. To make it persistent:

```bash
mkdir -p /var/log/journal
systemctl restart systemd-journald
```

Or edit `/etc/systemd/journald.conf` and set:
```ini
Storage=persistent
```

## rsyslogd — Traditional Logging

| File | Description |
|------|-------------|
| `/etc/rsyslog.conf` | Main rsyslog configuration file |
| `/etc/rsyslog.d/` | Drop-in config directory |
| `/var/log/messages` | General system messages |
| `/var/log/secure` | Authentication and security messages |
| `/var/log/cron` | Cron job logs |
| `/var/log/boot.log` | Boot messages |

| Command | Description |
|--------|-------------|
| `systemctl status rsyslog` | Check rsyslog service status |
| `systemctl restart rsyslog` | Restart after config changes |
| `logger "test message"` | Manually send a message to the log |


## logrotate — Managing Log Size

`logrotate` automatically rotates, compresses, and deletes old log files to prevent them from filling up the disk.

| File | Description |
|------|-------------|
| `/etc/logrotate.conf` | Main logrotate configuration |
| `/etc/logrotate.d/` | Per-application rotation configs |

```bash
logrotate -f /etc/logrotate.conf
# Force log rotation immediately
```

## Examples

```bash
journalctl -u sshd -f
# Watch SSH logs live

journalctl -p err -b
# Show all errors from this boot

journalctl --since "30 min ago"
# Show logs from the last 30 minutes

logger "Manual test log entry"
# Adds a line to /var/log/messages
```

## Key Takeaway

For the RHCSA, focus on `journalctl` — especially `-u`, `-f`, `-b`, `-p`, and `--since`. Know where rsyslog stores its files (`/var/log/messages`, `/var/log/secure`). Understand how to make the journal persistent by creating `/var/log/journal`.
