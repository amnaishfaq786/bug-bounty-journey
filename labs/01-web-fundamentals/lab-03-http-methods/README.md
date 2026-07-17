# Lab 03 – HTTP Methods

## Objective

Understand how HTTP methods communicate the client's intent and observe the differences between GET and POST requests using Burp Suite.

---

# Environment

- OS: Kali Linux
- Browser: Burp Suite Embedded Browser
- Tool: Burp Suite Community Edition
- Target: https://httpbin.org

---

# Tasks Performed

1. Intercepted a GET request using Burp Proxy.
2. Examined the HTTP request structure.
3. Sent the request to Burp Repeater.
4. Modified the request from GET to POST.
5. Added a request body.
6. Sent the modified request.
7. Observed the server's response.

---

# Evidence Collected

- get-request.txt
- post-request.txt
- post-response.json

---

# Key Observations

- GET requests retrieve resources.
- POST requests send data inside the request body.
- The request body begins after a blank line.
- Content-Type describes the body format.
- Content-Length specifies the body size in bytes.
- The server parsed the submitted form data successfully.

---

# Security Insight

Using the correct HTTP method is important.

GET requests should retrieve information only.

Applications that use GET for sensitive actions such as deleting accounts may expose themselves to vulnerabilities like Cross-Site Request Forgery (CSRF) if additional protections are not implemented.

---

# Conclusion

This lab demonstrated the structural differences between GET and POST requests. By manually editing and replaying requests in Burp Repeater, I gained a practical understanding of how HTTP methods, headers, and request bodies work together.
