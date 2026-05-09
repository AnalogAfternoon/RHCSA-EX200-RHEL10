# Lesson 27 — Securing RHEL with SELinux

> 📺 *Video coming soon!*

---

## Overview

SELinux (Security-Enhanced Linux) is a mandatory access control system built into RHEL. It provides an additional security layer beyond standard file permissions by labeling every file, process, and port with a context. Understanding SELinux is essential for the RHCSA exam.

---

## Subtopics

- 27.1 Understanding the Need for SELinux
- 27.2 How SELinux Uses Labels
- 27.3 Managing SELinux Modes
- 27.4 SELinux Component Overview
- 27.5 Exploring SELinux Working
- 27.6 Using File Context Labels
- 27.7 Finding the Right Context
- 27.8 Managing SELinux Port Access
- 27.9 Using Booleans
- 27.10 Troubleshooting SELinux

---

## SELinux Modes

| Mode | Description |
|------|-------------|
| Enforcing | SELinux policy is enforced — violations are blocked and logged |
| Permissive | Violations are logged but NOT blocked — useful for troubleshooting |
| Disabled | SELinux is completely off — not recommended |

```bash
getenforce
# Shows current mode: Enforcing, Permissive, or Disabled

setenforce 1
# Switch to Enforcing (temporary — resets on reboot)

setenforce 0
# Switch to Permissive (temporary — resets on reboot)
```

### Making Mode Changes Persistent

Edit `/etc/selinux/config`:
```
SELINUX=enforcing
```
Then reboot.

---

## SELinux Labels (Contexts)

Every file and process has an SELinux context with four parts:

```
user:role:type:level
system_u:object_r:httpd_sys_content_t:s0
```

The **type** is the most important part for day-to-day administration.

```bash
ls -Z /var/www/html/
# Shows SELinux context of files

ps -eZ | grep httpd
# Shows SELinux context of running processes
```

---

## Managing File Contexts

| Command | Description |
|--------|-------------|
| `ls -Z file` | View SELinux context of a file |
| `chcon -t type file` | Change context temporarily |
| `restorecon file` | Restore default context from policy |
| `restorecon -Rv /path/` | Recursively restore contexts |
| `semanage fcontext -l` | List all defined file context rules |
| `semanage fcontext -a -t type "/path(/.*)?"` | Add a persistent context rule |

```bash
# Example — set correct context for a custom web directory
semanage fcontext -a -t httpd_sys_content_t "/mywebsite(/.*)?"
restorecon -Rv /mywebsite/
```

---

## Managing Port Contexts

SELinux controls which ports services can use.

```bash
semanage port -l
# List all port contexts

semanage port -l | grep http
# Find HTTP-related port contexts

semanage port -a -t http_port_t -p tcp 8080
# Allow Apache to use port 8080

semanage port -d -t http_port_t -p tcp 8080
# Remove the port rule
```

---

## SELinux Booleans

Booleans are on/off switches that enable or disable specific SELinux policy behaviors without writing custom policy.

```bash
getsebool -a
# List all booleans and their current state

getsebool boolean_name
# Check a specific boolean

setsebool boolean_name on
# Turn a boolean on (temporary)

setsebool -P boolean_name on
# Turn a boolean on persistently (survives reboot)
```

### Common Booleans

| Boolean | Purpose |
|---------|---------|
| `httpd_can_network_connect` | Allow Apache to make network connections |
| `httpd_enable_homedirs` | Allow Apache to serve from home directories |
| `ftp_home_dir` | Allow FTP access to home directories |
| `samba_enable_home_dirs` | Allow Samba to share home directories |

---

## Troubleshooting SELinux

```bash
# Install troubleshooting tools
dnf install setroubleshoot-server

# View SELinux denial messages
ausearch -m avc -ts recent

# Get human-readable explanations and fix suggestions
sealert -a /var/log/audit/audit.log

# Check audit log directly
tail -f /var/log/audit/audit.log | grep denied
```

> 💡 **Tip:** When something is blocked and you suspect SELinux, run `setenforce 0` temporarily. If it works, SELinux was the cause — fix the context or boolean, then `setenforce 1`.

---

## Key Takeaway

SELinux is a major RHCSA exam topic. Know `getenforce`, `setenforce`, `ls -Z`, `restorecon`, `semanage fcontext`, `semanage port`, `getsebool`, and `setsebool -P`. The most common fix is running `restorecon` after moving files. Always use `-P` with `setsebool` to make changes persistent.
