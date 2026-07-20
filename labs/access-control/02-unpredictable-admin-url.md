# Lab 02 - Unprotected Admin Functionality with Unpredictable URL

## Difficulty
Apprentice

## Category
Access Control

## Overview
This lab demonstrates how relying on a hidden or unpredictable URL for administrative functionality is not a secure access control mechanism. Although the application attempted to hide the admin panel, the endpoint was exposed in client-side JavaScript and the server failed to enforce authorization.

## Objective
Locate the hidden administrator panel and delete the user `carlos`.

## Reconnaissance

The HTML source of the homepage was inspected to identify hidden functionality.

An inline JavaScript block contained the following code:

```javascript
var isAdmin = false;

if (isAdmin) {
    adminPanelTag.setAttribute('href', '/admin-h9780l');
}
```

Although the link was not displayed to normal users, the administrator endpoint was still exposed to anyone inspecting the page source.

## Vulnerability Analysis

The application relied on client-side logic to hide administrative functionality.

Because JavaScript is delivered to every user's browser, hidden URLs can be easily discovered. The server also failed to verify whether the user was authorized before granting access to the administrator panel.

This resulted in broken access control.

## Exploitation

1. Inspect the HTML source.
2. Locate the hidden administrator URL.
3. Browse to:

```
/admin-h9780l
```

4. Access the administrator panel.
5. Delete the user `carlos`.
6. Verify that the lab is solved.

## Root Cause

- Sensitive functionality was exposed in client-side code.
- Authorization checks were missing on the server.
- The application relied on security through obscurity instead of proper access control.

## Impact

An attacker can discover hidden administrative endpoints and perform privileged actions without authentication or authorization, potentially compromising the entire application.

## Key Takeaways

- Client-side code should never be trusted for access control.
- Hidden URLs are not a security mechanism.
- Authorization must always be enforced on the server.
- Always inspect HTML and JavaScript during reconnaissance.
