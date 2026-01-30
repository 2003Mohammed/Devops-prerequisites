from collections import Counter

with open("/var/log/syslog") as f:
    errors = [line for line in f if "error" in line.lower()]

print(Counter(errors).most_common(5))

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -- 
Use cases

Incident postmortems

Pattern detection

Cost-effective monitoring

python/09-python-api-he
