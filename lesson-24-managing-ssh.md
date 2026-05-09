# Lesson 24 — Managing SSH

> 📺 *Video coming soon!*

---

## Overview

SSH is the standard tool for secure remote access to Linux systems. This lesson goes deeper than basic connectivity — covering key-based authentication, SSH configuration options, and secure file transfer tools.

---

## Subtopics

- 24.1 Understanding SSH Key-based Login
- 24.2 Setting up SSH Key-based Login
- 24.3 Caching SSH Keys
- 24.4 Exploring Common SSH Server Options
- 24.5 Copying Files Securely
- 24.6 Synchronizing Files Securely

---

## SSH Key-based Login

Key-based login is more secure than password login. It uses a pair of cryptographic keys — a **private key** (kept on your machine) and a **public key** (placed on the remote server).

### Setting Up Key-based Login

```bash
# Step 1 — Generate a key pair
ssh-keygen
# Saves private key to ~/.ssh/id_rsa
# Saves public key to ~/.ssh/id_rsa.pub

# Step 2 — Copy public key to remote server
ssh-copy-id user@YOUR_SERVER_IP
# Adds your public key to ~/.ssh/authorized_keys on the server

# Step 3 — Connect without a password
ssh user@YOUR_SERVER_IP
```

---

## Caching SSH Keys — ssh-agent

If your private key has a passphrase, you can cache it so you don't have to type it every time.

```bash
# Start the agent
eval $(ssh-agent)

# Add your key to the agent
ssh-add ~/.ssh/id_rsa
# Enter passphrase once — cached for the session

# List cached keys
ssh-add -l
```

---

## SSH Server Configuration

The SSH server config file is `/etc/ssh/sshd_config`. Common options:

| Option | Description |
|--------|-------------|
| `Port 22` | The port SSH listens on |
| `PermitRootLogin no` | Disable direct root login |
| `PasswordAuthentication no` | Force key-based login only |
| `AllowUsers username` | Only allow specific users |
| `MaxAuthTries 3` | Limit failed login attempts |

```bash
# After editing sshd_config, restart the service
systemctl restart sshd

# Test config for errors before restarting
sshd -t
```

---

## Copying Files Securely — scp and sftp

### scp — Secure Copy

```bash
# Copy a file TO a remote server
scp file.txt user@YOUR_SERVER_IP:/home/user/

# Copy a file FROM a remote server
scp user@YOUR_SERVER_IP:/home/user/file.txt .

# Copy a directory recursively
scp -r mydir/ user@YOUR_SERVER_IP:/home/user/
```

### sftp — Secure FTP

```bash
sftp user@YOUR_SERVER_IP
# Opens an interactive session

# Inside sftp:
ls          # List remote files
lls         # List local files
get file    # Download a file
put file    # Upload a file
exit        # Close the session
```

---

## Synchronizing Files Securely — rsync

`rsync` is more efficient than `scp` for syncing — it only transfers changed files.

```bash
# Sync a local directory to a remote server
rsync -avz mydir/ user@YOUR_SERVER_IP:/home/user/mydir/

# Sync from remote to local
rsync -avz user@YOUR_SERVER_IP:/home/user/mydir/ mydir/

# rsync flags:
# -a = archive mode (preserves permissions, timestamps)
# -v = verbose
# -z = compress during transfer
```

---

## Key Takeaway

For the RHCSA, know how to set up key-based SSH login with `ssh-keygen` and `ssh-copy-id`. Know the important `sshd_config` options, especially `PermitRootLogin` and `PasswordAuthentication`. Know `scp` for quick transfers and `rsync` for efficient syncing.
