import shutil

total, used, free = shutil.disk_usage("/")
usage = used / total * 100

if usage > 80:
    print(f"Disk usage critical: {usage:.2f}%")
- - - - - - - - - - - - - - - - - -
Why Python here

Readable

Extensible (email, Slack, API later)
