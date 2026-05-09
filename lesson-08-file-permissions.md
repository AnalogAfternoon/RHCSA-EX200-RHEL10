# Lesson 8 — File Permissions

> 📺 *Video coming soon!*

---

## Overview

File permissions control who can read, write, and execute files in Linux. Every file has an owner, a group, and a set of permissions for three categories of users: the owner, the group, and everyone else (other).

---

## Viewing Permissions

```bash
ls -l
# Output example:
# -rwxr-xr-- 1 jason developers 1024 May 1 10:00 script.sh
#  |||||||||||
#  |||||||||++-- Other permissions (r--)
#  ||||||+++---- Group permissions (r-x)
#  |||+++------- Owner permissions (rwx)
#  ||+---------- File type (- = file, d = directory)
```

---

## chmod — Change Permissions

### Symbolic Method

| Command | Description |
|--------|-------------|
| `chmod u+x file` | Add execute permission for the owner |
| `chmod u-w file` | Remove write permission from the owner |
| `chmod g+r file` | Add read permission for the group |
| `chmod o-r file` | Remove read permission for others |
| `chmod a+x file` | Add execute permission for everyone |

**Who the letters refer to:**
- `u` — user (owner)
- `g` — group
- `o` — other
- `a` — all

### Numeric Method

| Command | Description |
|--------|-------------|
| `chmod 644 file` | rw-r--r-- — standard for regular files |
| `chmod 755 file` | rwxr-xr-x — standard for scripts and directories |
| `chmod 700 file` | rwx------ — owner only, full access |
| `chmod 600 file` | rw------- — owner read/write only |

---

## Permission Values

| Number | Permission | Symbol |
|--------|-----------|--------|
| 4 | Read | r |
| 2 | Write | w |
| 1 | Execute | x |
| 7 | Read + Write + Execute | rwx |
| 6 | Read + Write | rw- |
| 5 | Read + Execute | r-x |
| 4 | Read only | r-- |
| 0 | No permissions | --- |

> 💡 **How to calculate:** Add the values together. Read(4) + Write(2) = 6. Read(4) + Execute(1) = 5. Read(4) + Write(2) + Execute(1) = 7.

---

## chown & chgrp — Change Ownership

| Command | Description |
|--------|-------------|
| `chown user file` | Change the owner of a file |
| `chgrp group file` | Change the group of a file |
| `chown user:group file` | Change both owner and group at once |
| `chown -R user:group dir` | Recursively change ownership of a directory |

---

## Examples

```bash
ls -l script.sh
# -rw-r--r-- 1 jason jason 512 May 1 script.sh

chmod u+x script.sh
# Adds execute permission for the owner
# Now: -rwxr--r--

chmod 755 script.sh
# Sets rwxr-xr-x — owner can do everything, others can read and execute

chmod 644 notes.txt
# Sets rw-r--r-- — standard file permissions

chown root:root /etc/myconfig
# Changes owner and group to root

chown -R jason:developers /home/jason/projects/
# Recursively changes ownership of all files in the directory
```

---

## Key Takeaway

For the RHCSA, know both the symbolic method (`chmod u+x`) and the numeric method (`chmod 755`). The most common values to memorize are `755` for scripts and directories, `644` for regular files, and `700` for private files. Always think in three groups: **owner | group | other**.
