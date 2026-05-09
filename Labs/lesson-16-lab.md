# Lesson 16 Lab — Scheduling Tasks

Complete the following tasks. Do not refer to your notes.

---

1. Open your user's crontab for editing.

2. Add a cron job that runs `/scripts/backup.sh` every day at 2:00 AM.

3. Add a cron job that runs `/scripts/check.sh` every 15 minutes.

4. Add a cron job that runs `/scripts/weekly.sh` every Monday at 9:00 AM.

5. List your current crontab entries.

6. Schedule a one-time job to run the command `echo "test" >> /tmp/attest.txt` one minute from now using `at`.

7. List all pending `at` jobs.

8. Remove the pending `at` job you just created.

9. List all active systemd timers.

10. Place a script called `cleanup.sh` in the appropriate directory so it runs automatically every day via the system cron.
