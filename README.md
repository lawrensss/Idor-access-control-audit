# IDOR Access Control Audit

## Overview
This project documents a security assessment of a simulated employee portal where an Insecure Direct Object Reference (IDOR) vulnerability was identified.

This testing was performed in a controlled lab environment for educational purposes.

---

## What Was Tested

Authenticated access control validation.

The application used a URL parameter:

`?id=username`

The system did not verify that the authenticated session matched the requested ID.

---

## How the Issue Was Discovered

1. Logged in as a standard user
2. Observed profile request containing `?id=wiener`
3. Intercepted request using Burp Suite
4. Modified parameter to `id=administrator`
5. Server returned administrator data

---

## Root Cause

The application trusted user-controlled URL parameters without enforcing server-side authorization checks.

---

## Security Impact

- Privilege escalation
- Unauthorized data access
- Potential full system compromise

---

## Recommended Fix

- Implement strict server-side authorization
- Remove password autofill behavior
- Use UUIDs instead of predictable usernames
- Apply Zero Trust access validation

---

## Key Lesson

Authorization must always be enforced server-side.  
Client-side identifiers must never determine access control.
