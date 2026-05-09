# Lesson 30 — Preparing and Booking the Exam

> 📺 *Video coming soon!*

---

## Overview

The final lesson covers what to expect on exam day, how to book your RHCSA exam, and strategies for success. The RHCSA is a hands-on performance-based exam — there are no multiple choice questions.

---

## About the RHCSA Exam

| Detail | Info |
|--------|------|
| Exam name | Red Hat Certified System Administrator (EX200) |
| Duration | 3 hours |
| Format | Hands-on, performance-based — no multiple choice |
| Passing score | 210 out of 300 (70%) |
| Environment | Live RHEL system — tasks must work when graded |
| Delivery | Remote proctored or in-person at a testing center |

---

## How to Book the Exam

1. Go to [redhat.com](https://www.redhat.com/en/services/certification)
2. Create or log in to your Red Hat account
3. Search for **EX200** — RHCSA exam
4. Choose remote proctored or testing center
5. Select a date and time
6. Complete payment

> 💡 Red Hat occasionally offers discounted exam vouchers through bundles or promotions — check before purchasing at full price.

---

## Key Topics to Review Before the Exam

| Topic | Lessons |
|-------|---------|
| Command line basics | Lessons 1–2 |
| File management | Lessons 3–4 |
| Users, groups, permissions | Lessons 7–8 |
| Software management | Lesson 12 |
| Processes and systemd | Lessons 13–15 |
| Storage — partitions and LVM | Lessons 18–19 |
| Boot procedure and troubleshooting | Lessons 20–22 |
| SSH and networking | Lessons 24, 28 |
| SELinux | Lesson 27 |
| Scheduling and automation | Lessons 16, 23 |

---

## Exam Day Tips

- **Practice in a lab environment** — set up a RHEL or Rocky Linux VM and work through tasks without notes
- **Read each task carefully** — partial credit is given, but tasks often depend on each other
- **Use `man` pages** — the exam allows it; know how to search them with `man -k` and `/`
- **Verify your work** — after completing a task, test it (restart services, check status, reboot and verify persistence)
- **Manage your time** — 3 hours goes fast; don't spend too much time on one task
- **Persistence matters** — if a service or setting must survive a reboot, make sure it does (`systemctl enable`, fstab entries, `setsebool -P`, etc.)

---

## Practice Lab Checklist

Before exam day, make sure you can do all of the following without notes:

- [ ] Create users, set passwords, lock/unlock accounts
- [ ] Set file permissions with chmod and chown (numeric and symbolic)
- [ ] Configure and mount partitions with `/etc/fstab`
- [ ] Create and extend LVM logical volumes
- [ ] Install and remove software with `dnf`
- [ ] Enable and disable services with `systemctl`
- [ ] Write a basic bash script with variables and conditionals
- [ ] Configure SSH key-based login
- [ ] Set SELinux contexts with `semanage` and `restorecon`
- [ ] Open firewall ports and services with `firewall-cmd`
- [ ] Schedule tasks with `cron` and `at`
- [ ] Reset a forgotten root password using `rd.break`

---

## Key Takeaway

The RHCSA is about doing, not memorizing. The best preparation is practice — set up a VM, wipe it, and do it again. Everything in this course has been building toward this exam. You have the notes, you have the knowledge — now go practice until it's second nature. Good luck!
