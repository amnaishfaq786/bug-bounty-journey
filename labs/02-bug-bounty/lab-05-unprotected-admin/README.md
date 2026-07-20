# Lab 05 – Unprotected Admin Functionality

## Lab Information

Platform: PortSwigger Web Security Academy

Category: Access Control

Difficulty: Apprentice

Status: Solved

---

## Objective

Identify an administrator interface that is accessible without authentication and demonstrate the impact by deleting the user `carlos`.

---

## Skills Practiced

- Reconnaissance
- robots.txt enumeration
- Hidden endpoint discovery
- Access control verification
- Impact validation
- Burp Suite navigation

---

## Vulnerability

**Unprotected Administrative Functionality**

The administrator panel was publicly accessible without authentication or authorization checks.

---

## Impact

An attacker could:

- Access administrator functionality
- Delete users
- Perform privileged administrative actions

---

## Result

The administrator panel was discovered through `robots.txt`.

The user `carlos` was successfully deleted.

The lab was solved successfully.
