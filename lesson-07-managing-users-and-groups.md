# Lesson 7 — Managing Users and Groups

## Overview

User and group management is a core responsibility of any Linux system administrator. This lesson covers creating, modifying, and deleting users and groups, as well as managing passwords and account security.

## Creating & Deleting Users

| Command | Description |
|--------|-------------|
| `sudo useradd username` | Create a new user |
| `sudo useradd -G group username` | Create a user and add them to a group |
| `sudo userdel username` | Delete a user |
| `sudo userdel -r username` | Delete a user and their home directory |

## Modifying Users

| Command | Description |
|--------|-------------|
| `sudo usermod -c "comment" username` | Add a description or comment to a user account |
| `sudo usermod -aG group username` | Add a user to a group without removing from others |
| `sudo usermod -s /bin/bash username` | Change a user's default shell |
| `sudo usermod -L username` | Lock a user account |
| `sudo usermod -U username` | Unlock a user account |
| `sudo usermod -l newname username` | Rename a user |

> ⚠️ **Important:** Always use `-aG` (append to group) instead of just `-G` when adding a user to a group. Using `-G` alone will remove the user from all other groups.

## Passwords & Aging

| Command | Description |
|--------|-------------|
| `sudo passwd username` | Set or change a user's password |
| `sudo chage -M days username` | Set the maximum number of days before password must change |
| `sudo chage -l username` | List all password aging information for a user |

## Groups

| Command | Description |
|--------|-------------|
| `sudo groupadd groupname` | Create a new group |
| `sudo groupdel groupname` | Delete a group |


## Key System Files

| File | Description |
|------|-------------|
| `/etc/passwd` | Stores user account information (username, UID, home dir, shell) |
| `/etc/shadow` | Stores encrypted passwords and aging info |
| `/etc/group` | Stores group names and their members |

## Examples

```bash
sudo useradd jason
# Creates a new user named jason

sudo passwd jason
# Prompts you to set jason's password

sudo usermod -aG wheel jason
# Adds jason to the wheel (sudo) group

sudo usermod -L jason
# Locks jason's account — they can no longer log in

sudo chage -M 90 jason
# Requires jason to change their password every 90 days

sudo chage -l jason
# Shows all password aging details for jason

sudo userdel -r jason
# Deletes jason and removes their home directory
```

## Key Takeaway

User management is a guaranteed topic on the RHCSA. Know `useradd`, `usermod`, `userdel`, `passwd`, and `chage` by heart. Always use `-aG` when adding to groups. Know which file stores what — `/etc/passwd`, `/etc/shadow`, and `/etc/group`.
