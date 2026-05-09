# Lesson 16 Lab — Solutions

1. Open crontab for editing.
```bash
crontab -e
```

2. Run backup.sh daily at 2:00 AM.
```
0 2 * * * /scripts/backup.sh
```

3. Run check.sh every 15 minutes.
```
*/15 * * * * /scripts/check.sh
```

4. Run weekly.sh every Monday at 9:00 AM.
```
0 9 * * 1 /scripts/weekly.sh
```

5. List crontab entries.
```bash
crontab -l
```

6. Schedule a one-time at job.
```bash
echo 'echo "test" >> /tmp/attest.txt' | at now + 1 minute
```

7. List pending at jobs.
```bash
atq
```

8. Remove the at job (replace 1 with your job number).
```bash
atrm 1
```

9. List active systemd timers.
```bash
systemctl list-timers
```

10. Place script in daily cron directory.
```bash
sudo cp cleanup.sh /etc/cron.daily/
sudo chmod +x /etc/cron.daily/cleanup.sh
```
