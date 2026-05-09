# Lesson 28 — Configuring a Firewall

## Overview

RHEL uses `firewalld` as its firewall management tool. It uses zones and services to control what network traffic is allowed. This lesson covers how to analyze network connections and configure firewall rules.

## Subtopics

- 28.1 Analyzing Service Configuration with ss
- 28.2 Managing RHEL Firewalling
- 28.3 Exploring Firewalld Components
- 28.4 Allowing Service Access
- 28.5 Allowing Port Access
- 28.6 Exploring Advanced Firewalld Use

## Analyzing Network Connections — ss

`ss` replaces the older `netstat` command for viewing network socket information.

| Command | Description |
|--------|-------------|
| `ss -tulnp` | Show all listening TCP/UDP ports with process names |
| `ss -t` | Show TCP connections |
| `ss -u` | Show UDP connections |
| `ss -l` | Show listening sockets only |

```bash
ss -tulnp
# Output shows port, protocol, state, and which process is listening
# t=TCP, u=UDP, l=listening, n=numeric, p=process
```

## firewalld — Firewall Management

| Command | Description |
|--------|-------------|
| `systemctl status firewalld` | Check firewall status |
| `systemctl enable --now firewalld` | Enable and start firewalld |
| `firewall-cmd --state` | Quick check if firewalld is running |
| `firewall-cmd --list-all` | Show all current firewall rules |
| `firewall-cmd --get-zones` | List all available zones |
| `firewall-cmd --get-default-zone` | Show the default zone |


## Firewalld Zones

Zones define trust levels for network connections. The most common zones:

| Zone | Description |
|------|-------------|
| `public` | Default zone — untrusted networks |
| `trusted` | All traffic is allowed |
| `drop` | All incoming traffic is silently dropped |
| `internal` | For internal networks — more trusted than public |
| `dmz` | For DMZ servers — limited access |

## Allowing Services

Services are predefined firewall rules by name (http, ssh, ftp, etc.).

```bash
# List all available predefined services
firewall-cmd --get-services

# Allow a service temporarily (lost on reload)
firewall-cmd --add-service=http

# Allow a service permanently (survives reboot)
firewall-cmd --permanent --add-service=http
firewall-cmd --reload

# Remove a service
firewall-cmd --permanent --remove-service=http
firewall-cmd --reload
```

## Allowing Ports

```bash
# Allow a specific port permanently
firewall-cmd --permanent --add-port=8080/tcp
firewall-cmd --reload

# Allow a port range
firewall-cmd --permanent --add-port=8080-8090/tcp
firewall-cmd --reload

# Remove a port
firewall-cmd --permanent --remove-port=8080/tcp
firewall-cmd --reload
```

## Advanced Firewalld Use

### Rich Rules — More Granular Control

```bash
# Allow SSH only from a specific IP
firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="192.168.1.50" service name="ssh" accept'

# Block a specific IP
firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="10.0.0.5" reject'

firewall-cmd --reload
```

### Listing Everything

```bash
firewall-cmd --list-all
# Shows: zone, interfaces, services, ports, rich rules

firewall-cmd --list-services
# Shows only allowed services

firewall-cmd --list-ports
# Shows only allowed ports
```

## Important Rules

> ⚠️ Always use `--permanent` for rules you want to keep after reboot, then follow with `--reload` to apply them immediately.

> ⚠️ Without `--permanent`, rules are active until the next `firewall-cmd --reload` or system reboot.


## Key Takeaway

For the RHCSA, know `firewall-cmd --permanent --add-service=` and `--add-port=` cold, always followed by `--reload`. Know how to list current rules with `--list-all`. Use `ss -tulnp` to see what ports are listening before deciding what to open. Firewall misconfigurations are a common reason services are unreachable.
