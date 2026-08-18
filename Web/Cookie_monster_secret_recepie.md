# Cookie Monster Secret Recipe

**Category:** Web Exploitation

## Solution

* Submitted random credentials and received a hint to check cookies.
* Inspected **Browser DevTools → Application → Cookies** and found a `secret_recipe` cookie.
* The value was **Base64 encoded**.
* Decoded it using Burp Decoder/CyberChef to retrieve the flag.

## Concept

**Cookies** store client-side data sent with HTTP requests. Sensitive information should not be stored in cookies simply encoded with Base64, since Base64 is encoding, not encryption.

**Key Takeaway:** Always inspect cookies when investigating web applications.

**Tools:** Browser DevTools, Burp Suite/CyberChef
