# Monitoring and Observability Fundamentals for DevOps

Monitoring and observability are core DevOps practices used to detect system failures, troubleshoot production issues, and maintain reliability in real-world environments.

---

## 1. Monitoring vs Observability

Monitoring focuses on detecting known problems using predefined metrics and alerts. It answers what is failing.

Observability focuses on understanding system behavior by correlating metrics, logs, and traces. It answers why something is failing.

Monitoring detects issues. Observability helps resolve them.

---

## 2. Critical Metrics to Monitor

Every production system should track:

- CPU usage
- Memory utilization
- Disk usage and I/O
- Network latency and packet drops
- Application error rates
- Request response time

Missing any of these metrics can delay incident diagnosis.

---

## 3. Linux System Monitoring Commands

Common commands used during performance degradation:

```bash
top
uptime
free -m
df -h
iostat
````

These commands quickly reveal resource bottlenecks.

---

## 4. Process and Service Troubleshooting

Check running processes:

```bash
ps aux | grep nginx
```

Check service status:

```bash
systemctl status nginx
systemctl is-active docker
```

Restart failed services:

```bash
sudo systemctl restart nginx
```

Service validation is always done before deeper debugging.

---

## 5. Log Monitoring and Analysis

Logs provide historical context around failures.

Common log paths:

* /var/log/syslog
* /var/log/messages
* /var/log/nginx/access.log
* /var/log/nginx/error.log

Log analysis commands:

```bash
tail -f /var/log/syslog
grep ERROR /var/log/app.log
journalctl -u docker
```

Logs should be reviewed before restarting applications.

---

## 6. Application Health Checks

Applications expose endpoints for monitoring systems:

* /health
* /status
* /metrics

Manual validation example:

```bash
curl http://localhost:8080/health
```

These endpoints are used by load balancers and orchestrators.

---

## 7. Alerting Fundamentals

Good alerts:

* Represent user-impacting issues
* Require immediate action
* Avoid unnecessary noise

Poor alerts:

* Trigger frequently
* Focus only on resource spikes
* Cause alert fatigue

Alert quality directly impacts on-call effectiveness.

---

## 8. Common Monitoring Tools

Widely used tools in DevOps environments:

* Prometheus for metrics
* Grafana for visualization
* ELK Stack for centralized logging
* CloudWatch for AWS monitoring

Most production systems use multiple tools together.

---

## 9. Basic Monitoring Automation Script

Simple disk usage monitoring script:

```bash
#!/bin/bash

THRESHOLD=80
USAGE=$(df / | tail -1 | awk '{print $5}' | sed 's/%//')

if [ "$USAGE" -gt "$THRESHOLD" ]; then
  echo "WARNING: Disk usage exceeded ${USAGE}%"
fi
```

Such scripts are often executed using cron jobs.

---

## 10. Operational DevOps Mindset

* Monitor systems from the user’s perspective
* Correlate metrics with logs during incidents
* Faster diagnosis reduces downtime and MTTR

A system that cannot be observed cannot be operated reliably.


