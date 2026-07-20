# Lessons Learned

## Summary

This lab demonstrates an **Unprotected Administrative Functionality** vulnerability, a common form of **Broken Access Control**.

The objective is to identify an administrator interface that is accessible without authentication and verify its impact by performing an administrative action.

In this lab, the administrator panel was discovered through reconnaissance and the user `carlos` was successfully deleted, confirming the vulnerability.

---

# Learning Objectives

After completing this lab, the learner should be able to:

- Perform basic reconnaissance against a web application.
- Understand the purpose of `robots.txt`.
- Identify hidden application endpoints.
- Verify access control on sensitive functionality.
- Assess the impact of broken access control.
- Document findings using a professional reporting methodology.

---

# Key Concepts

## 1. Reconnaissance Before Exploitation

Effective bug bounty hunting begins with understanding the target application.

Before attempting to exploit any vulnerability, publicly accessible resources should be enumerated to identify interesting functionality.

Examples include:

- robots.txt
- sitemap.xml
- JavaScript files
- Burp Suite Site Map
- HTTP headers
- Public endpoints

---

## 2. robots.txt Is Not a Security Control

The application contained:

```
User-agent: *
Disallow: /administrator-panel
```

The `robots.txt` file provides guidance to search engine crawlers and does **not** restrict user access.

Sensitive resources must never rely on `robots.txt` for protection.

---

## 3. Hidden Does Not Mean Protected

The administrator interface was not linked from the application but remained directly accessible.

Security through obscurity is not an effective defense.

Every sensitive endpoint must enforce proper authentication and authorization.

---

## 4. Broken Access Control

The administrator panel accepted requests from unauthenticated users.

No authentication or authorization checks were performed before granting access to privileged functionality.

This represents a classic Broken Access Control vulnerability.

---

## 5. Demonstrating Impact

The vulnerability was confirmed by successfully deleting the user `carlos`.

Demonstrating impact is an essential step in validating a security finding.

---

# Professional Bug Bounty Methodology

1. Read and understand the target.
2. Perform reconnaissance.
3. Enumerate accessible resources.
4. Identify sensitive functionality.
5. Verify access control.
6. Demonstrate impact.
7. Document evidence.
8. Report findings.

---

# Common Mistakes

- Assuming hidden URLs are secure.
- Treating `robots.txt` as an access control mechanism.
- Skipping reconnaissance.
- Reporting hidden endpoints without verifying exploitability.
- Failing to demonstrate impact.

---

# Skills Developed

- Web application reconnaissance
- Endpoint enumeration
- robots.txt analysis
- Access control assessment
- Burp Suite navigation
- Vulnerability validation
- Security reporting
- Technical documentation

---

# Conclusion

Administrative functionality must always be protected by robust authentication and authorization mechanisms.

Sensitive endpoints should never rely on hidden URLs or crawler directives for security.

This lab establishes the foundation for identifying and assessing Broken Access Control vulnerabilities in real-world bug bounty engagements.
