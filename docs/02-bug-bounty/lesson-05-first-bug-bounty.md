# Lesson 5 – First Real Bug Bounty Engagement

## Objective

Complete the first authorized Web Security Academy lab using a professional bug bounty methodology.

---

## Target

Platform: PortSwigger Web Security Academy

Category: Access Control

Lab: Unprotected admin functionality

Difficulty: Apprentice

---

## Methodology

Instead of immediately attacking the application, the following workflow was used:

1. Read the lab description.
2. Perform reconnaissance.
3. Identify interesting endpoints.
4. Verify access control.
5. Demonstrate impact.
6. Document findings.

Workflow:

Observe
↓

Understand
↓

Test
↓

Verify
↓

Document

---

## Reconnaissance

Visited:

/robots.txt

Discovered:

Disallow: /administrator-panel

This revealed a hidden administrator endpoint.

---

## Vulnerability

The administrator panel was accessible without authentication.

No authorization checks were enforced.

An unauthenticated user could perform administrative actions.

---

## Exploitation

Visited:

/administrator-panel

Deleted user:

carlos

The lab was successfully solved.

---

## Security Impact

An attacker could:

- Access administrator functionality
- Delete users
- Perform privileged actions
- Completely bypass authorization

---

## Key Takeaways

- robots.txt is not a security mechanism.
- Hidden URLs are not protected URLs.
- Sensitive functionality must always enforce authorization.
- Reconnaissance is the first phase of every bug bounty engagement.
