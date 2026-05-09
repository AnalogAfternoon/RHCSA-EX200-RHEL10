# Lesson 12 — Managing Software

## Overview

Managing software on RHEL means working with RPM packages, DNF repositories, and modern packaging tools like Flatpak. This lesson covers everything from installing individual packages to managing repositories and updates.


## Subtopics

- 12.1 Understanding DNF and Flatpak Use Cases
- 12.2 Managing RPM Packages
- 12.3 Setting up Repository Access
- 12.4 Managing Packages with dnf
- 12.5 Using dnf Groups
- 12.6 Managing dnf Updates and History
- 12.7 Using subscription-manager
- 12.8 Installing Software with Flatpak
- 12.9 Managing Flatpak Applications


## DNF — Package Manager

| Command | Description |
|--------|-------------|
| `dnf install package` | Install a package |
| `dnf remove package` | Remove a package |
| `dnf update` | Update all installed packages |
| `dnf update package` | Update a specific package |
| `dnf search keyword` | Search for a package by keyword |
| `dnf info package` | Show details about a package |
| `dnf list installed` | List all installed packages |
| `dnf history` | View dnf transaction history |
| `dnf history undo ID` | Undo a specific transaction |

## DNF Groups

| Command | Description |
|--------|-------------|
| `dnf group list` | List all available package groups |
| `dnf group install "Group Name"` | Install an entire group of packages |
| `dnf group remove "Group Name"` | Remove a package group |

## RPM — Package Tool

| Command | Description |
|--------|-------------|
| `rpm -qa` | List all installed RPM packages |
| `rpm -qi package` | Show detailed info about an installed package |
| `rpm -ql package` | List all files installed by a package |
| `rpm -qf /path/to/file` | Find which package owns a file |

## Repository Management

| Command | Description |
|--------|-------------|
| `dnf repolist` | List all enabled repositories |
| `dnf repolist all` | List all repositories including disabled |
| `dnf config-manager --add-repo URL` | Add a new repository |
| `subscription-manager register` | Register system with Red Hat |
| `subscription-manager repos --list` | List available repositories |
| `subscription-manager repos --enable repo-id` | Enable a specific repository |

## Flatpak

| Command | Description |
|--------|-------------|
| `flatpak install app` | Install a Flatpak application |
| `flatpak list` | List installed Flatpak apps |
| `flatpak update` | Update all Flatpak applications |
| `flatpak remove app` | Remove a Flatpak application |


## Examples

```bash
dnf install vim
# Installs the vim text editor

dnf search nmap
# Searches for nmap in available repositories

rpm -qf /etc/passwd
# Finds which package owns the /etc/passwd file

dnf group list
# Shows all available software groups

dnf history
# Shows all past install/remove transactions

subscription-manager register --username user --password pass
# Registers system with Red Hat subscription
```


## Key Takeaway

For the RHCSA, focus on `dnf install`, `dnf remove`, `dnf update`, and `dnf group install`. Know how to set up repository access and use `rpm -qf` to trace which package owns a file. `subscription-manager` is important for real RHEL environments.
