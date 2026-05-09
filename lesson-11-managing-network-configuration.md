# Lesson 11 — Managing Network Configuration

> 📺 *Video coming soon!*

---

## Overview

Network configuration is essential for any Linux administrator. This lesson covers IPv4 and IPv6 networking concepts, how to configure interfaces using NetworkManager tools, and how to troubleshoot connectivity issues.

---

## Subtopics

- 11.1 Understanding IPv4 Networking
- 11.2 Exploring IPv6 Networking
- 11.3 Understanding NIC Naming
- 11.4 Defining Host Names and Host Name Resolution
- 11.5 Analyzing Network Configuration
- 11.6 Understanding NetworkManager
- 11.7 Managing Network Configuration with nmcli
- 11.8 Managing Network Configuration with nmtui
- 11.9 Troubleshooting Networking

---

## IPv4 Networking Basics

| Concept | Description |
|---------|-------------|
| IP Address | Unique address for a device (e.g. 192.168.1.10) |
| Subnet Mask | Defines the network portion (e.g. 255.255.255.0 = /24) |
| Default Gateway | Router IP — where traffic goes when leaving the local network |
| DNS Server | Resolves hostnames to IP addresses |

---

## NIC Naming

RHEL uses **predictable network interface names** instead of the old eth0, eth1 style.

| Prefix | Type |
|--------|------|
| `eno` | Onboard NIC |
| `enp` | PCI NIC (slot-based) |
| `ens` | Hotplug NIC |
| `wlo` | Onboard wireless |

```bash
ip link show
# Lists all network interfaces and their names
```

---

## Viewing Network Configuration

| Command | Description |
|--------|-------------|
| `ip addr` | Show all IP addresses |
| `ip addr show dev enp0s3` | Show IP for a specific interface |
| `ip route` | Show routing table |
| `ip link show` | Show interface status (up/down) |
| `ss -tulnp` | Show listening ports |
| `cat /etc/resolv.conf` | Show DNS servers |

---

## Hostname Management

| Command | Description |
|--------|-------------|
| `hostname` | Show current hostname |
| `hostnamectl` | Show full hostname information |
| `hostnamectl set-hostname name` | Set the system hostname permanently |

```bash
hostnamectl set-hostname rhel-server.example.com
```

### Host Name Resolution Files

| File | Description |
|------|-------------|
| `/etc/hostname` | Stores the system hostname |
| `/etc/hosts` | Local hostname-to-IP mapping |
| `/etc/resolv.conf` | DNS server configuration |

```bash
# Add a local hostname resolution entry
echo "192.168.1.20  webserver.local" >> /etc/hosts
```

---

## NetworkManager

NetworkManager is the service that manages network connections on RHEL. It stores connection profiles and handles interface configuration automatically.

```bash
systemctl status NetworkManager
# Check if NetworkManager is running

nmcli general status
# Show overall NetworkManager status
```

---

## nmcli — Command Line Network Manager

### Viewing Connections

```bash
nmcli connection show
# List all saved connection profiles

nmcli device status
# Show all network devices and their state

nmcli connection show "connection-name"
# Show detailed info about a specific connection
```

### Configuring a Static IP

```bash
nmcli connection modify "enp0s3" \
  ipv4.addresses 192.168.1.100/24 \
  ipv4.gateway 192.168.1.1 \
  ipv4.dns 8.8.8.8 \
  ipv4.method manual

nmcli connection up "enp0s3"
# Apply the new settings
```

### Configuring DHCP

```bash
nmcli connection modify "enp0s3" ipv4.method auto
nmcli connection up "enp0s3"
```

### Creating a New Connection

```bash
nmcli connection add \
  type ethernet \
  con-name "my-connection" \
  ifname enp0s3 \
  ipv4.method auto
```

---

## nmtui — Text User Interface

A simple menu-driven interface for NetworkManager — easier than nmcli for basic tasks.

```bash
nmtui
# Opens an interactive menu to edit connections, set hostname, etc.
```

---

## Troubleshooting Networking

```bash
ping 8.8.8.8
# Test basic connectivity to the internet

ping google.com
# Test DNS resolution + connectivity

traceroute 8.8.8.8
# Trace the path packets take to a destination

ip route
# Check the routing table — verify default gateway

dig google.com
# Test DNS resolution

nslookup google.com
# Alternative DNS test

nmcli connection show
# Check if connection profile is configured correctly

journalctl -u NetworkManager -f
# Watch NetworkManager logs live
```

---

## Key Takeaway

For the RHCSA, know `nmcli connection modify` for setting static IPs and `nmcli connection up` to apply changes. Know `ip addr`, `ip route`, and `ping` for basic diagnostics. Know how to set the hostname with `hostnamectl set-hostname`. NetworkManager is always running on RHEL — don't edit config files directly, use nmcli or nmtui.
