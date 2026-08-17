# Secret Box

**Category:** Web Exploitation

## Solution

* Created an account and logged in.
* The challenge hint suggested **SQL Injection**, so I tested the secret input with `'`.
* The resulting database error confirmed SQL injection.
* Inspected the source code and found the admin's `owner_id`.
* Used a PostgreSQL SQLi payload to retrieve the admin's secret:

```text
' || (SELECT content FROM secrets WHERE owner_id='ADMIN_OWNER_ID') || '
```

* The response revealed the flag.

## Concept

**SQL Injection:** Occurs when user input is directly incorporated into SQL queries, allowing an attacker to modify the intended query and access unauthorized database data.

**Key Takeaway:** Database errors can reveal useful information about the underlying query and database structure.

**Tools:** Browser, Source Code, SQL
