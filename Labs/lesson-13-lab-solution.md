# Lesson 13 Lab — Solutions

1. Display all running processes.
```bash
ps aux
```

2. Find `sshd` process.
```bash
ps aux | grep sshd
```

3. Run `sleep 300` in background.
```bash
sleep 300 &
```

4. List background jobs.
```bash
jobs
```

5. Bring job to foreground.
```bash
fg %1
```

6. Suspend then send to background.
```bash
# Press Ctrl+Z to suspend
bg %1
```

7. Display memory in human-readable format.
```bash
free -h
```

8. Show uptime and load averages.
```bash
uptime
```

9. Open top, sort by memory, then quit.
```bash
top
# Press M to sort by memory
# Press q to quit
```

10. Display CPU info.
```bash
lscpu
```
