# 01 – Why Monitoring Matters in DevOps

## Purpose
Monitoring is not optional in DevOps.  
Without monitoring, failures are detected by users, not engineers.

This file explains **what monitoring actually solves** in real systems.

---

## What Monitoring Answers

Monitoring helps answer:
- Is the system running?
- Is it slow or overloaded?
- Is it about to fail?
- What changed before the failure?

---

## Monitoring vs Observability

- Monitoring tells you **something is wrong**
- Observability helps you understand **why it is wrong**

DevOps relies on both.

---

## Core Monitoring Areas

Every production system must monitor:
- CPU usage
- Memory usage
- Disk usage
- Network traffic
- Application health
- Logs

Ignoring any one of these creates blind spots.

---

## Real DevOps Scenario

Problem: Application is slow  
Without monitoring: Guesswork  
With monitoring: High memory usage → OOM kills → restart loop

---

## Key Takeaway
Monitoring turns failures into **data-driven decisions**, not panic.

