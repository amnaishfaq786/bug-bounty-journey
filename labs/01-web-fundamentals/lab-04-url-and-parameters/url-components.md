# Practical 1 - URL Components

## Objective

Learn the structure of a URL.

---

## Example URL

https://shop.example.com:443/products?id=25#reviews

---

## Components

| Component | Value |
|-----------|-------|
| Scheme | https |
| Host | shop.example.com |
| Port | 443 |
| Path | /products |
| Query String | id=25 |
| Fragment | #reviews |

---

## Observation

A URL contains multiple components, each serving a different purpose.

The browser sends the scheme, host, path, and query string to the server.

The fragment remains inside the browser.

---

## Conclusion

Understanding URL structure is essential before testing web applications because different URL components are processed by different parts of the system.
