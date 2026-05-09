# Lesson 6 — Root Privileges and SSH

## Overview

Most administrative tasks in Linux require elevated privileges. This lesson covers how to safely gain root access and how to connect to and transfer files between remote machines using SSH.

## Privilege Escalation

| Command | Description |
|--------|-------------|
| `sudo command` | Run a single command as root |
| `sudo su -` | Fully switch to the root user session |
| `su username` | Switch to another user account |
| `exit` | Return to the previous user |

> 💡 **Tip:** Notice the shell prompt changes from `$` (regular user) to `#` (root) when you switch to root. This is a quick visual indicator of who you are.

## SSH — Secure Remote Access

SSH lets you connect to and control remote Linux machines securely over a network.

| Command | Description |
|--------|-------------|
| `ssh user@IP` | Connect to a remote machine |
| `scp file user@IP:path` | Copy a file TO a remote machine |
| `scp user@IP:file /local/path` | Copy a file FROM a remote machine |

## Examples

```bash
sudo dnf update
# Runs a system update as root without switching users

sudo su -
# Fully switches to root — notice the prompt changes to #

exit
# Returns to your regular user account

su jason
# Switches to the user "jason"

ssh jason@YOUR_SERVER_IP
# Connects to a remote machine at that IP address

scp notes.txt jason@YOUR_SERVER_IP:/home/jason/
# Copies notes.txt to the remote machine's home directory

scp jason@YOUR_SERVER_IP:/home/jason/notes.txt .
# Copies notes.txt FROM the remote machine to your current directory
```

## Key Takeaway

`sudo` is safer than logging in as root directly because it logs every command run with elevated privileges. For the RHCSA, know the difference between `sudo command` (one command as root) and `sudo su -` (full root session). SSH and SCP are essential skills for managing remote servers.
