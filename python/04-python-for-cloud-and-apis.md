# Python for Cloud and APIs

## HTTP Requests
import requests

r = requests.get("https://api.github.com")
print(r.status_code)

## JSON
data = r.json()

## DevOps Use Case
Used for CI/CD APIs, monitoring tools, cloud services.
