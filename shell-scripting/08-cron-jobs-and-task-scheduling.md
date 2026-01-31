
# 08 – Cron Jobs and Task Scheduling for DevOps

## Overview

In real-world DevOps environments, **automation does not end with scripts**. Scripts must be **scheduled, monitored, and controlled**.
Cron is the backbone of scheduled automation on Linux systems, commonly used for:

* Log rotation and cleanup
* Backups and snapshots
* Health checks
* Periodic sync jobs
* Cost-control and housekeeping tasks

This file focuses on **production-safe cron usage**, common pitfalls, and real DevOps patterns.

---

## What is Cron?

Cron is a **time-based job scheduler** in Unix-like systems.
It runs commands or scripts at predefined times without manual intervention.

Key components:

* `cron` → the daemon (service)
* `crontab` → user-specific schedule configuration
* `/etc/cron.*` → system-wide scheduled jobs

---

## Cron Time Format (Critical for DevOps)

```
* * * * * command
| | | | |
| | | | └── Day of week (0–7, Sun=0 or 7)
| | | └──── Month (1–12)
| | └────── Day of month (1–31)
| └──────── Hour (0–23)
└────────── Minute (0–59)
```

### Examples

```bash
0 2 * * * /path/to/backup.sh
```

➡ Runs daily at **02:00 AM**

```bash
*/5 * * * * /path/to/health-check.sh
```

➡ Runs every **5 minutes**

```bash
0 0 * * 0 /path/to/weekly-cleanup.sh
```

➡ Runs every **Sunday at midnight**

---

## Managing Cron Jobs

### View current cron jobs

```bash
crontab -l
```

### Edit cron jobs

```bash
crontab -e
```

### Remove all cron jobs (⚠ dangerous)

```bash
crontab -r
```

---

## Production Rule #1: NEVER rely on environment variables

Cron runs with a **minimal environment**.

❌ This will often fail:

```bash
python script.py
```

✅ Always use full paths:

```bash
/usr/bin/python3 /opt/scripts/script.py
```

Check paths using:

```bash
which python3
```

---

## Logging Cron Jobs (Mandatory in DevOps)

Cron **does not log output by default**.

### Basic logging

```bash
0 * * * * /opt/scripts/job.sh >> /var/log/job.log 2>&1
```

### Timestamped logging (recommended)

```bash
0 * * * * /opt/scripts/job.sh >> /var/log/job.log 2>&1
```

Inside the script:

```bash
echo "$(date '+%F %T') | Job started"
```

---

## Safe Cron Script Template (DevOps Standard)

```bash
#!/usr/bin/env bash
set -euo pipefail

LOG_FILE="/var/log/disk-monitor.log"

log() {
  echo "$(date '+%F %T') | $1" >> "$LOG_FILE"
}

log "Cron job started"

df -h / | awk 'NR==2 {print $5}' | sed 's/%//' | {
  read usage
  if [ "$usage" -gt 80 ]; then
    log "Disk usage critical: $usage%"
  else
    log "Disk usage normal: $usage%"
  fi
}

log "Cron job finished"
```

---

## Common DevOps Cron Use Cases

### 1. Disk Cleanup (Prevent Outages)

```bash
0 1 * * * find /var/log -type f -mtime +14 -delete
```

➡ Prevents disk-full incidents.

---

### 2. Service Health Monitoring

```bash
*/2 * * * * systemctl is-active nginx || systemctl restart nginx
```

➡ Self-healing pattern (use cautiously).

---

### 3. Backup Automation

```bash
0 3 * * * tar -czf /backups/etc-$(date +\%F).tar.gz /etc
```

---

### 4. CI Agent Cleanup

```bash
0 */6 * * * rm -rf /tmp/ci-build-*
```

➡ Prevents CI runners from filling disks.

---

## Debugging Cron Issues (Very Important)

### Check cron service

```bash
systemctl status cron
```

### Check cron logs

```bash
grep CRON /var/log/syslog
```

or

```bash
journalctl -u cron
```

---

## Common Cron Failures (Real Incidents)

### ❌ Script works manually, fails in cron

**Reason:** Missing PATH or permissions.

**Fix:**

* Use absolute paths
* Add execute permission

```bash
chmod +x script.sh
```

---

### ❌ Cron runs but nothing happens

**Reason:** No logging.

**Fix:** Redirect stdout & stderr.

---

### ❌ Script overlaps and causes damage

**Fix:** Locking mechanism

```bash
flock -n /tmp/job.lock /opt/scripts/job.sh
```

---

## System-wide Cron vs User Cron

| Type              | Use Case              |
| ----------------- | --------------------- |
| `crontab -e`      | User-level automation |
| `/etc/crontab`    | System maintenance    |
| `/etc/cron.daily` | Daily housekeeping    |

---

## DevOps Best Practices for Cron

* One responsibility per script
* Always log output
* Never hardcode secrets
* Prefer monitoring tools for critical jobs
* Document cron jobs (README or comments)

---

## Interview Insight

> Cron is powerful but dangerous. In modern DevOps, cron is often replaced by **CI/CD schedulers, Kubernetes CronJobs, or cloud-native schedulers**, but **cron knowledge is still mandatory for Linux-based systems**.

---

## Summary

Cron is not just scheduling — it is **automation reliability**.
A good DevOps engineer treats cron jobs like production code:
**versioned, logged, tested, and monitored**.


