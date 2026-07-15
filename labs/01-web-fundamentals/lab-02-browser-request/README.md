# Lab 02 – Browser Request Interception

## Objective

Capture a browser HTTP request using Burp Suite and understand the information sent by modern web browsers.

---

## Tools Used

- Kali Linux
- Burp Suite Community Edition
- Chromium Browser

---

## Target

https://example.com

---

## Procedure

1. Started Burp Suite.
2. Opened Burp Browser.
3. Turned **Intercept ON**.
4. Visited https://example.com.
5. Burp intercepted the browser request.
6. Modified the `Accept-Language` header from:

```http
en-US,en;q=0.9
```

to

```http
fr
```

7. Forwarded the request.
8. Observed the response.

---

## Observation

The response was still returned in English.

Reason:

The server ignored the language preference and returned its default language.

---

## Lesson Learned

The client can request preferences.

The server decides what it will return.

This demonstrates why changing client-side data does not necessarily change server behavior.

---

## Security Insight

An attacker can modify:

- HTTP Headers
- Cookies
- URL Parameters
- Request Body
- HTTP Method

Therefore,

**Servers must validate every client request.**
