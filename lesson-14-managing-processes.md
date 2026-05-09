# Lesson 14 — Managing Processes

## Overview

Monitoring processes is one thing — actively managing them is another. This lesson covers how to send signals to control processes, adjust their priority, apply performance profiles, and manage user sessions.

## Subtopics

- 14.1 Using Signals to Manage Process State
- 14.2 Managing Process Priority
- 14.3 Using tuned Profiles
- 14.4 Managing User Sessions and Processes

## Signals — Controlling Processes

| Command | Description |
|--------|-------------|
| `kill PID` | Send SIGTERM (graceful stop) to a process |
| `kill -9 PID` | Send SIGKILL (force kill) to a process |
| `kill -l` | List all available signals |
| `killall processname` | Kill all processes with that name |
| `pkill processname` | Kill processes matching a name pattern |

### Common Signals

| Signal | Number | Meaning |
|--------|--------|---------|
| SIGTERM | 15 | Gracefully request termination |
| SIGKILL | 9 | Forcefully terminate — cannot be ignored |
| SIGHUP | 1 | Hangup — often used to reload config |
| SIGSTOP | 19 | Pause a process |
| SIGCONT | 18 | Resume a paused process |

## Process Priority — nice and renice

Linux assigns each process a priority from **-20 (highest)** to **19 (lowest)**. Default is 0.

| Command | Description |
|--------|-------------|
| `nice -n value command` | Start a command with a specific priority |
| `renice value -p PID` | Change priority of a running process |
| `ps -el` | View processes with their priority (NI column) |

> ⚠️ Only root can set negative (higher priority) nice values.

## tuned — Performance Profiles

`tuned` is a system daemon that automatically optimizes performance based on a selected profile.

| Command | Description |
|--------|-------------|
| `tuned-adm list` | List all available profiles |
| `tuned-adm active` | Show the currently active profile |
| `tuned-adm profile profile-name` | Apply a specific profile |
| `tuned-adm recommend` | Get the recommended profile for your system |

### Common Profiles

| Profile | Use Case |
|---------|----------|
| `balanced` | General use — balance of power and performance |
| `throughput-performance` | Maximum throughput for servers |
| `latency-performance` | Low latency workloads |
| `powersave` | Minimize power consumption |
| `virtual-guest` | Optimized for virtual machines |

## Managing User Sessions

| Command | Description |
|--------|-------------|
| `loginctl list-sessions` | List all active user sessions |
| `loginctl list-users` | List logged-in users |
| `loginctl terminate-session ID` | End a specific user session |
| `w` | Show who is logged in and what they are doing |
| `who` | List currently logged-in users |

## Examples

```bash
kill -9 1234
# Force kills the process with PID 1234

killall firefox
# Kills all firefox processes

nice -n 10 tar -czf backup.tar.gz /home/
# Runs tar with lower priority so it doesn't slow the system

renice 5 -p 2345
# Lowers priority of running process 2345

tuned-adm recommend
# Output: throughput-performance

tuned-adm profile throughput-performance
# Applies the recommended profile

loginctl list-sessions
# Shows all active login sessions
```

## Key Takeaway

For the RHCSA, know `kill`, `kill -9`, `nice`, `renice`, and `tuned-adm`. The difference between SIGTERM (polite) and SIGKILL (force) is a common exam concept. `tuned` profiles are also exam-relevant — know how to list, check, and apply them.
