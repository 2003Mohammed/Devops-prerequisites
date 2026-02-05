# 03 – Log Monitoring and Troubleshooting Basics

## Purpose
Logs record **what actually happened inside a system**.
They are essential for debugging issues that metrics alone cannot explain.

---

## What Logs Represent

Logs capture:
- Errors
- Warnings
- State changes
- Application behavior over time

They provide **historical context** during failures.

---

## Why Logs Are Critical in DevOps

DevOps teams rely on logs to:
- Investigate incidents
- Trace failures back to root causes
- Validate system behavior after changes

Without logs, troubleshooting becomes assumption-based.

---

## Logs vs Metrics

- Metrics indicate **that** something is wrong
- Logs explain **why** it is wrong

Both are required for effective operations.

---

## Real DevOps Scenario

Issue: Service crashes intermittently  
Metrics appear normal  
Logs reveal: Configuration parsing error during startup

---

## Key Takeaway
Logs are the primary source of truth during incidents and must always be accessible and reliable.

