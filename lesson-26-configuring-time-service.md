# Lesson 26 — Configuring Time Service

## Overview

Accurate time is critical for logging, authentication, certificates, and scheduled tasks. This lesson covers how to manage time on RHEL using `timedatectl`, the `date` command, and NTP (Network Time Protocol) for synchronization.

## Subtopics

- 26.1 Exploring Linux Time
- 26.2 Setting Time with timedatectl
- 26.3 Using date
- 26.4 Managing an NTP Client
- 26.5 Managing an NTP Server

## timedatectl — System Time Management

| Command | Description |
|--------|-------------|
| `timedatectl` | Show current date, time, timezone, and NTP status |
| `timedatectl set-time "YYYY-MM-DD HH:MM:SS"` | Set the date and time manually |
| `timedatectl set-timezone Region/City` | Set the timezone |
| `timedatectl list-timezones` | List all available timezones |
| `timedatectl set-ntp true` | Enable NTP synchronization |
| `timedatectl set-ntp false` | Disable NTP synchronization |

```bash
timedatectl
# Output example:
#               Local time: Mon 2024-01-15 10:30:00 EST
#           Universal time: Mon 2024-01-15 15:30:00 UTC
#                 RTC time: Mon 2024-01-15 15:30:00
#                Time zone: America/New_York (EST, -0500)
# System clock synchronized: yes
#               NTP service: active

timedatectl set-timezone America/New_York
# Sets timezone to Eastern Time

timedatectl list-timezones | grep America
# Lists all American timezones
```

## date — Display and Set Time

```bash
date
# Shows current date and time

date "+%Y-%m-%d %H:%M:%S"
# Custom format output

date -s "2024-01-15 10:30:00"
# Set date/time manually (not recommended when NTP is active)
```

## NTP — Network Time Protocol

NTP keeps your system clock synchronized with internet time servers. RHEL uses **chronyd** as its NTP implementation.

### Managing chronyd

| Command | Description |
|--------|-------------|
| `systemctl status chronyd` | Check chronyd service status |
| `systemctl enable --now chronyd` | Enable and start chronyd |
| `chronyc tracking` | Show current time sync status |
| `chronyc sources` | Show NTP sources being used |
| `chronyc makestep` | Force immediate time sync |

### NTP Client Configuration

Edit `/etc/chrony.conf`:

```bash
# Add or change NTP servers
server time.cloudflare.com iburst
server pool.ntp.org iburst

# After editing:
systemctl restart chronyd
```

### NTP Server Configuration

To make your RHEL system an NTP server for other machines, add to `/etc/chrony.conf`:

```bash
# Allow clients from your local network
allow 192.168.1.0/24

# Then restart
systemctl restart chronyd

# Open firewall for NTP
firewall-cmd --permanent --add-service=ntp
firewall-cmd --reload
```

## Key Takeaway

For the RHCSA, know `timedatectl` for checking and setting time and timezone, and know that `chronyd` is the NTP service on RHEL. Be able to configure `/etc/chrony.conf` to point to specific NTP servers. Time sync issues can cause authentication and certificate failures — always verify NTP is active.
