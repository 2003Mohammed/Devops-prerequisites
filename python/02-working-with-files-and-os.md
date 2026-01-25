# Working with Files and OS

import os

## List Files
os.listdir(".")

## Environment Variables
os.environ.get("HOME")

## Files
with open("file.txt", "r") as f:
    print(f.read())

## Create File
with open("new.txt", "w") as f:
    f.write("hello")

## DevOps Use Case
Used for config files, logs, state files.
