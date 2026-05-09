# Lesson 9 — Managing Users and Groups

> 📺 *Video coming soon!*

---

## Overview

Every user on a Linux system has an account with properties that define who they are and what they can access. This lesson covers how to create and manage users and groups, set default behaviors, and control account access.

---

## Subtopics

- 9.1 Understanding the Purpose of User Accounts
- 9.2 Exploring User Properties
- 9.3 Creating and Managing Users
- 9.4 Defining User Default Settings
- 9.5 Limiting User Access
- 9.6 Managing Group Membership
- 9.7 Creating and Managing Groups
- 9.8 Managing Password Properties

---

## User Properties

Each user account has properties stored in `/etc/passwd`:

```
username:password:UID:GID:comment:home_dir:shell
jason:x:1001:1001:Jason Smith:/home/jason:/bin/bash
```

| Field | Description |
|-------|-------------|
| username | Login name |
| password | `x` means password is in `/etc/shadow` |
| UID | User ID number |
| GID | Primary group ID |
| comment | Full name or description |
| home_dir | Home directory path |
| shell | Default login shell |

---

## Creating and Managing Users

| Command | Description |
|--------|-------------|
| `useradd username` | Create a new user with defaults |
| `useradd -m -s /bin/bash username` | Create user with home dir and bash shell |
| `useradd -G group username` | Create user and add to a supplementary group |
| `usermod -aG group username` | Add existing user to a group |
| `usermod -s /bin/bash username` | Change user's shell |
| `usermod -L username` | Lock a user account |
| `usermod -U username` | Unlock a user account |
| `userdel username` | Delete a user |
| `userdel -r username` | Delete user and their home directory |

---

## User Default Settings

| File/Dir | Description |
|----------|-------------|
| `/etc/default/useradd` | Default settings applied when creating users |
| `/etc/login.defs` | System-wide login and password policies |
| `/etc/skel/` | Template files copied to new user home directories |

```bash
useradd -D
# Show current default settings for useradd

cat /etc/login.defs
# Shows password aging, UID/GID ranges, and other policies
```

---

## Limiting User Access

| Command | Description |
|--------|-------------|
| `usermod -L username` | Lock account — user cannot log in |
| `usermod -e YYYY-MM-DD username` | Set account expiration date |
| `chage -M days username` | Set max days before password must change |
| `chage -l username` | List password aging information |
| `chage -E YYYY-MM-DD username` | Set account expiration date |

---

## Managing Groups

| Command | Description |
|--------|-------------|
| `groupadd groupname` | Create a new group |
| `groupmod -n newname oldname` | Rename a group |
| `groupdel groupname` | Delete a group |
| `usermod -aG groupname username` | Add user to a group |
| `gpasswd -d username groupname` | Remove user from a group |
| `groups username` | Show all groups a user belongs to |
| `id username` | Show UID, GID, and all group memberships |

---

## Key System Files

| File | Description |
|------|-------------|
| `/etc/passwd` | User account information |
| `/etc/shadow` | Encrypted passwords and aging info |
| `/etc/group` | Group names and members |
| `/etc/gshadow` | Secure group account information |

---

## Managing Password Properties

| Command | Description |
|--------|-------------|
| `passwd username` | Set or change a user's password |
| `passwd -l username` | Lock the password |
| `passwd -u username` | Unlock the password |
| `chage -M 90 username` | Password must change every 90 days |
| `chage -m 7 username` | Minimum 7 days between password changes |
| `chage -W 14 username` | Warn user 14 days before expiration |

---

## Key Takeaway

For the RHCSA, know `useradd`, `usermod`, `userdel`, `groupadd`, `groupdel`, `passwd`, and `chage` cold. Always use `-aG` when adding a user to a group to avoid removing them from existing groups. Know which file stores what — `/etc/passwd`, `/etc/shadow`, and `/etc/group`.
