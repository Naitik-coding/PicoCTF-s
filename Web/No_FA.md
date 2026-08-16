# No FA

**Category:** Web Exploitation

## Solution

* Found a leaked `users.db` containing the admin password hash.
* The password used an **unsalted SHA-256 hash**, which could be cracked to obtain the password.
* Logged in as `admin` and reached the 2FA page.
* Inspected the Flask session cookie and decoded it, revealing the `otp_secret`.
* Used the OTP from the session to bypass 2FA and retrieve the flag.

## Concepts

**Unsalted Hashing** — Without a unique salt, identical passwords produce identical hashes, making dictionary attacks and precomputed hash lookups easier.

**Flask Session** — Flask's default session is stored client-side in a signed cookie. If sensitive values such as an OTP are stored in it, they may be exposed even though the cookie is protected against tampering.

**2FA Logic Flaw** — 2FA becomes ineffective when the OTP secret is exposed to the client instead of being securely maintained server-side.

**Key Takeaway:** Never store sensitive authentication secrets such as OTPs in client-accessible session data.
