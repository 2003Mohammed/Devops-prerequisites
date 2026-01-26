# Real-World Python DevOps Scripts

## Disk Check
import shutil
total, used, free = shutil.disk_usage("/")
print(free)

## Health Check
import socket
socket.gethostbyname("google.com")

## DevOps Use Case
Monitoring, automation, infrastructure validation.
