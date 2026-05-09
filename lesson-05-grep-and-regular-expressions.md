# Lesson 5 — grep and Regular Expressions

> 📺 *Video coming soon!*

---

## Overview

`grep` is one of the most used commands in Linux. It searches through text — files, command output, logs — and returns only the lines that match what you are looking for. Combined with regular expressions, it becomes an incredibly powerful filter.

---

## Basic grep

| Command | Description |
|--------|-------------|
| `grep "word" file` | Search for a word in a file |
| `grep -i "word" file` | Case-insensitive search |
| `grep -v "word" file` | Invert match — show lines that do NOT contain the word |
| `grep -c "word" file` | Count the number of matching lines |
| `grep -r "word" /dir` | Recursively search all files in a directory |

---

## Regular Expressions

Regular expressions (regex) let you search for patterns, not just exact words.

| Pattern | Description |
|--------|-------------|
| `grep "^word" file` | Lines that start with "word" |
| `grep "word$" file` | Lines that end with "word" |
| `grep "[0-9]" file` | Lines containing any digit |
| `grep "[a-z]" file` | Lines containing any lowercase letter |
| `grep -E "a\|b" file` | Lines matching "a" or "b" — extended regex |

---

## Examples

```bash
grep "root" /etc/passwd
# Finds all lines containing "root" in the passwd file

grep -i "error" /var/log/messages
# Finds errors regardless of uppercase or lowercase

grep -v "nologin" /etc/passwd
# Shows only users that have a real login shell

grep "^jason" /etc/passwd
# Finds lines that start with "jason"

grep "[0-9]" /etc/passwd
# Finds lines that contain at least one number

grep -c "bash" /etc/passwd
# Counts how many users have bash as their shell

grep -r "sshd" /etc/
# Searches every file in /etc for "sshd"

cat /etc/passwd | grep "bash"
# Pipes passwd output into grep — same result, different style
```

---

## Key Takeaway

`grep` is essential for the RHCSA — especially for searching config files and log files. Practice combining it with pipes. Know `^` (starts with), `$` (ends with), `-i` (case insensitive), `-v` (invert), and `-r` (recursive) cold.
