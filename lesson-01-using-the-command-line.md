# Lesson 1 — Using the Command Line

> 📺 *Video coming soon!*

---

## Overview

Before you can do anything meaningful in Linux, you need to know how to navigate the command line. These five commands are the foundation of everything — you will use them in every single session.

---

## Commands

| Command | Description |
|--------|-------------|
| `pwd` | Print working directory — shows where you currently are |
| `ls` | List files and folders in the current directory |
| `ls -l` | Detailed list with permissions, size, owner, and date |
| `cd` | Change directory — move to a different location |
| `whoami` | Display which user you are currently logged in as |

---

## Examples

```bash
pwd
# Output: /home/jason

ls
# Output: Documents  Downloads  notes.txt

ls -l
# Output: -rw-r--r-- 1 jason jason 1024 May 1 10:00 notes.txt

cd /etc
# Moves into the /etc directory

cd ..
# Moves up one directory level

whoami
# Output: jason
```

---

## Key Takeaway

These are the most basic navigation commands in Linux. You will use them constantly — memorize them early. Think of `pwd` as "where am I?", `ls` as "what's here?", and `cd` as "take me there."
