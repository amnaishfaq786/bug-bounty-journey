# Access Control

## Overview

Access control determines what actions an authenticated or unauthenticated user is allowed to perform within an application. Proper access control ensures that users can only access resources and functionality they are authorized to use.

Broken access control is one of the most common and impactful web application vulnerabilities because it can allow attackers to access sensitive information or perform administrative actions.

---

## Types of Access Control

### Vertical Access Control
Restricts functionality based on user roles.

Example:

- User
- Moderator
- Administrator

A normal user should never access administrator functionality.

---

### Horizontal Access Control

Restricts users from accessing another user's resources.

Example:

- User A should not be able to view User B's account.

---

### Context-Dependent Access Control

Access depends on the current state of the application.

Examples:

- Password reset workflows
- Multi-step checkout
- Approval processes

---

## Common Vulnerabilities

- Unprotected administrative functionality
- Hidden administrative URLs
- Insecure Direct Object References (IDOR)
- Forced browsing
- Missing authorization checks
- Client-side access control
- Privilege escalation

---

## Testing Methodology

When testing access control:

1. Map application functionality.
2. Inspect HTML and JavaScript.
3. Look for hidden endpoints.
4. Attempt direct access.
5. Modify identifiers.
6. Test with different user roles.
7. Verify whether authorization is enforced on the server.

---

## Lessons Completed

| Lab | Topic | Status |
|------|-------|--------|
| 01 | Unprotected Admin Functionality | ✅ |
| 02 | Unprotected Admin Functionality with Unpredictable URL | ✅ |

---

## Key Principles

- Never trust client-side code.
- Hidden URLs are not security.
- Always enforce authorization on the server.
- Security through obscurity is not a defense.
