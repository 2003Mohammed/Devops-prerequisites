# Running Shell Commands with Python

import subprocess

## Run Command
subprocess.run(["ls", "-l"])

## Capture Output
result = subprocess.run(
    ["df", "-h"],
    capture_output=True,
    text=True
)

print(result.stdout)

## DevOps Use Case
Used in automation frameworks and tools.
