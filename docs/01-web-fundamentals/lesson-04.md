# Lesson 04 - URLs and Parameters

## Objective

Learn how a URL is structured, understand which parts are sent to the server, and practice modifying query parameters using Burp Suite.

---

## URL Structure

Example:

https://shop.example.com:443/products?id=25#reviews

| Component | Value | Purpose |
|-----------|-------|---------|
| Scheme | https | Protocol used for communication |
| Host | shop.example.com | Server/domain |
| Port | 443 | HTTPS port |
| Path | /products | Requested resource |
| Query String | id=25 | Data sent to the server |
| Fragment | #reviews | Browser-only navigation |

---

## Query Parameters

Query parameters begin after the `?`.

Example:

/get?id=25&name=amna

Parameters are key-value pairs:

id=25

name=amna

Multiple parameters are separated by `&`.

---

## Fragment

Example:

https://httpbin.org/get#reviews

Intercepted request:

GET /get HTTP/1.1

Observation:

The browser removed `#reviews` before sending the request.

Conclusion:

Fragments are processed by the browser and are not transmitted to the server.

---

## Parameter Tampering

Original request:

GET /get?id=25&name=amna HTTP/1.1

Modified request in Burp Repeater:

GET /get?id=99&name=hacker HTTP/1.1

Server response:

{
    "args": {
        "id": "99",
        "name": "hacker"
    }
}

Observation:

The server received the modified values exactly as they were sent.

---

## Security Insight

Users completely control their own HTTP requests.

Applications must validate every parameter received from clients.

Changing a parameter does not create a vulnerability by itself. A vulnerability exists only if the server trusts or authorizes modified values incorrectly.

---

## Reflection

This lesson demonstrated that Burp Suite can intercept and modify HTTP requests before they reach the server. Query parameters are fully controlled by the client, while fragments remain inside the browser and never reach the server.

---

## Key Takeaways

- URLs have multiple components.
- Fragments are not sent to servers.
- Query parameters are transmitted in the request line.
- Clients can modify query parameters.
- Servers must validate all client-supplied input.
