# Lesson 10 — Securing Files with Permissions

> 📺 *Video coming soon!*

---

## Overview

Linux file permissions control exactly who can read, write, and execute files and directories. This lesson goes deeper than basic permissions — covering ownership, default permissions, special bits, and shared group directories.

---

## Subtopics

- 10.1 Understanding File Ownership
- 10.2 Changing File Ownership
- 10.3 Understanding Basic Permissions
- 10.4 Managing Basic Permissions
- 10.5 Applying Default Permissions
- 10.6 Configuring Directories for Shared Group Access

---

## Understanding File Ownership

Every file has an **owner** (user) and a **group owner**. Permissions apply separately to three categories:

```bash
ls -l file.txt
# -rw-r--r-- 1 jason developers 1024 May 1 file.txt
#  |||||||||||   |||||  ||||||||||
#  |||||||||||   owner  group
#  |||||||++++-- other permissions (r--)
#  ||||++++------ group permissions (r--)
#  |++++--------- owner permissions (rw-)
#  +------------- file type
```

---

## Changing Ownership

| Command | Description |
|--------|-------------|
| `chown user file` | Change the owner of a file |
| `chown user:group file` | Change both owner and group |
| `chown -R user:group dir` | Recursively change ownership |
| `chgrp group file` | Change only the group |

```bash
chown jason:developers project/
chown -R jason:developers /var/www/mysite/
```

---

## Basic Permissions

| Permission | File | Directory |
|-----------|------|-----------|
| r (4) | Read file contents | List directory contents |
| w (2) | Modify file | Create/delete files in directory |
| x (1) | Execute file | Enter (cd into) directory |

---

## Managing Permissions — chmod

### Symbolic Method

```bash
chmod u+x file      # Add execute for owner
chmod g-w file      # Remove write from group
chmod o+r file      # Add read for others
chmod a+x file      # Add execute for everyone
chmod u+x,g-w file  # Multiple changes at once
```

### Numeric Method

```bash
chmod 644 file   # rw-r--r-- — standard file
chmod 755 file   # rwxr-xr-x — standard script/dir
chmod 700 file   # rwx------ — private
chmod 640 file   # rw-r----- — owner read/write, group read
```

---

## Default Permissions — umask

`umask` defines what permissions are **removed** from newly created files and directories.

```bash
umask
# Output: 0022 — this is the default

# With umask 022:
# New files get:       644 (rw-r--r--)
# New directories get: 755 (rwxr-xr-x)
```

| umask | New File | New Directory |
|-------|----------|---------------|
| 022 | 644 | 755 |
| 027 | 640 | 750 |
| 077 | 600 | 700 |

```bash
# Set umask for current session
umask 027

# Make permanent — add to ~/.bashrc or /etc/profile
echo "umask 027" >> ~/.bashrc
```

---

## Special Permission Bits

### SUID (Set User ID) — on executables

```bash
chmod u+s file
chmod 4755 file
# File runs with the owner's permissions, not the caller's
# Example: /usr/bin/passwd runs as root even when called by a regular user
ls -l /usr/bin/passwd
# -rwsr-xr-x  (s in owner execute position = SUID)
```

### SGID (Set Group ID) — on directories

```bash
chmod g+s directory
chmod 2755 directory
# Files created inside inherit the directory's group
# Used for shared group directories
```

### Sticky Bit — on directories

```bash
chmod +t directory
chmod 1777 directory
# Users can only delete their own files in the directory
# Example: /tmp uses the sticky bit
ls -ld /tmp
# drwxrwxrwt  (t in other execute position = sticky bit)
```

---

## Configuring Directories for Shared Group Access

To set up a directory where a group can collaborate:

```bash
# Step 1 — Create the directory
mkdir /shared/project

# Step 2 — Set the group owner
chown :developers /shared/project

# Step 3 — Set permissions and SGID
chmod 2770 /shared/project
# 2 = SGID, 7 = owner full, 7 = group full, 0 = others nothing
# New files will automatically belong to the developers group
```

---

## Key Takeaway

For the RHCSA, know both symbolic and numeric chmod. Understand umask and how it affects default permissions. Know SUID, SGID, and sticky bit — especially SGID on shared directories. The shared group directory setup (`chown :group`, `chmod 2770`) is a common exam task.
