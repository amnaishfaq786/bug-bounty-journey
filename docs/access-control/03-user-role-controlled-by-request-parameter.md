# User Role Controlled by Request Parameter

## Overview

This document explains the theory behind a **Broken Access Control** vulnerability where an application determines a user's privileges using client-controlled data. In this lab, the application relied on a cookie named `Admin` to decide whether a user was an administrator.

Since cookies are stored in the client's browser, they can be modified before being sent to the server. If the server trusts these values without validation, an attacker can escalate their privileges.

---

# Learning Objectives

After completing this topic, you should understand:

* What client-controlled authorization is.
* Why authorization must always be enforced on the server.
* How to identify authorization-related parameters during reconnaissance.
* How to safely test authorization using Burp Suite.
* How to prevent this vulnerability in real-world applications.

---

# Understanding the Vulnerability

Authentication and authorization serve different purposes.

* **Authentication** answers: **Who are you?**
* **Authorization** answers: **What are you allowed to do?**

Once a user is authenticated, the server should determine their permissions using trusted server-side data.

A vulnerable application instead trusts data supplied by the client, for example:

```http
Cookie: Admin=false
```

Because the browser controls cookies, an attacker can modify the value before sending the request.

Example:

```http
Cookie: Admin=true
```

If the server grants administrator privileges based solely on this value, the application is vulnerable to privilege escalation.

---

# Why This Is Insecure

Everything stored in the browser is under the user's control.

Attackers can modify:

* Cookies
* URL parameters
* Hidden form fields
* Local storage
* Session storage
* Custom HTTP headers

None of these should be trusted when making authorization decisions.

Authorization should always be verified on the server using the authenticated session.

---

# Common Indicators During Testing

While performing reconnaissance, look for values such as:

```text
Admin=false
role=user
isAdmin=0
privilege=guest
access=user
userRole=member
```

Finding these values does **not** automatically indicate a vulnerability, but they are strong candidates for further testing.

---

# Testing Methodology

A professional penetration tester should follow a structured process:

## 1. Authenticate

Log in using a normal user account.

---

## 2. Capture Requests

Use Burp Suite Proxy to intercept authenticated requests.

---

## 3. Identify Interesting Parameters

Look for client-controlled values that appear related to authorization.

Examples include:

* Cookies
* URL parameters
* Hidden fields
* JSON properties
* HTTP headers

---

## 4. Form a Hypothesis

Ask:

> "What happens if this value is modified?"

Only change **one parameter at a time**.

---

## 5. Replay the Request

Use Burp Repeater to send the modified request.

Compare the response with the original request.

---

## 6. Verify Access

Look for evidence such as:

* New navigation links
* Administrator pages
* Additional functionality
* Different HTTP status codes
* More data returned in the response

---

## 7. Confirm the Vulnerability

Attempt to access privileged functionality.

If access is granted without legitimate permissions, the application contains a Broken Access Control vulnerability.

---

# Security Impact

A successful attack may allow an attacker to:

* Escalate privileges
* Access administrator functionality
* Modify application data
* Delete user accounts
* Bypass authorization checks
* Compromise the application

The severity is typically **High** because authorization failures often lead to complete application compromise.

---

# Prevention

Developers should:

* Store only a session identifier in cookies.
* Store user roles on the server.
* Validate authorization on every privileged request.
* Never trust client-controlled values.
* Apply the principle of least privilege.
* Log and monitor privileged actions.

---

# Key Takeaways

* Authentication and authorization are different concepts.
* Client-controlled data must never determine user privileges.
* Cookies should identify a session, not define permissions.
* Burp Repeater is an effective tool for testing authorization logic.
* Change one parameter at a time to accurately identify vulnerabilities.
* Every privileged endpoint must perform server-side authorization checks.
