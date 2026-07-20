# Finding Report

## Title

Unauthenticated Access to Administrator Panel

---

## Severity

High

---

## Category

Broken Access Control

---

## Description

The application exposes an administrator interface that is accessible without authentication.

An unauthenticated user can directly access the administrator panel and perform privileged administrative actions.

---

## Steps to Reproduce

1. Visit:

   /robots.txt

2. Observe:

   ```
   User-agent: *
   Disallow: /administrator-panel
   ```

3. Browse to:

   ```
   /administrator-panel
   ```

4. Verify that the administrator interface is accessible without logging in.

5. Click **Delete** next to the user **carlos**.

---

## Evidence

The administrator panel was accessible without authentication.

The user **carlos** was successfully deleted.

The lab status changed to **Solved**.

---

## Impact

An attacker could:

- Access administrator functionality
- Delete users
- Modify administrative data
- Perform privileged operations without authentication

---

## Root Cause

The administrator endpoint does not enforce authentication or authorization before allowing access.

---

## Recommendation

Sensitive administrative functionality should:

- Require user authentication.
- Verify that the authenticated user has administrator privileges.
- Return **403 Forbidden** for unauthorized users.
- Never rely on hidden URLs or `robots.txt` to protect sensitive resources.
