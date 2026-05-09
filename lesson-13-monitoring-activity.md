# Lesson 13 — Monitoring Activity

> 📺 *Video coming soon!*

---

## Overview

As a system administrator, knowing how to observe what is happening on your system is critical. This lesson covers how to monitor jobs, processes, memory, and CPU activity using essential Linux tools.

---

## Subtopics

- 13.1 Exploring Jobs and Processes
- 13.2 Managing Shell Jobs
- 13.3 Understanding Process States
- 13.4 Observing Process Information with ps
- 13.5 Monitoring Memory Usage
- 13.6 Observing CPU Load
- 13.7 Monitoring System Activity with top

---

## Jobs and Processes

| Command | Description |
|--------|-------------|
| `jobs` | List all background jobs in the current shell |
| `bg %job` | Resume a stopped job in the background |
| `fg %job` | Bring a background job to the foreground |
| `command &` | Run a command in the background |
| `Ctrl+Z` | Suspend (pause) a running process |
| `Ctrl+C` | Terminate a running process |

## Process States

| State | Meaning |
|-------|---------|
| R | Running or runnable |
| S | Sleeping (waiting for an event) |
| D | Uninterruptible sleep (usually I/O) |
| Z | Zombie (finished but not cleaned up) |
| T | Stopped |

## ps — Process Information

| Command | Description |
|--------|-------------|
| `ps` | Show processes for the current shell |
| `ps aux` | Show all processes for all users |
| `ps aux | grep process` | Find a specific process |
| `ps -ef` | Show full process listing with parent IDs |

## Memory Monitoring

| Command | Description |
|--------|-------------|
| `free -m` | Show memory usage in megabytes |
| `free -h` | Show memory usage in human-readable format |
| `cat /proc/meminfo` | Detailed memory information |

## CPU Load

| Command | Description |
|--------|-------------|
| `uptime` | Show system uptime and load averages |
| `cat /proc/loadavg` | Show raw load average data |
| `lscpu` | Display CPU architecture information |

## top — Live System Monitor

| Key | Action inside top |
|-----|------------------|
| `top` | Launch the live process monitor |
| `q` | Quit top |
| `k` | Kill a process (enter PID when prompted) |
| `M` | Sort by memory usage |
| `P` | Sort by CPU usage |
| `1` | Show individual CPU core stats |

---

## Examples

```bash
ps aux | grep sshd
# Finds if the SSH daemon is running

free -h
# Shows memory in GB/MB — easy to read

uptime
# Output: 10:00 up 3 days, load average: 0.10, 0.15, 0.12

top
# Opens live monitor — press q to quit

sleep 100 &
# Runs sleep in the background

jobs
# Shows: [1]+ Running sleep 100 &

fg %1
# Brings sleep back to the foreground
```

---

## Key Takeaway

For the RHCSA, know `ps aux`, `top`, and `free -h` — these are the go-to tools for checking what is running and how resources are being used. Understanding process states (especially zombie and sleeping) is also exam-relevant.
