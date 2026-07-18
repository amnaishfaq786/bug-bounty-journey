# Practical 4 - Parameter Tampering

## Objective

Modify query parameters using Burp Suite Repeater and verify that the server receives the modified values.

---

## Original Request

```http
GET /get?id=25&name=amna HTTP/1.1
Host: postman-echo.com
```

---

## Modified Request

```http
GET /get?id=99&name=hacker HTTP/1.1
Host: postman-echo.com
```

---

## Server Response

```json
{
  "args": {
    "id": "99",
    "name": "hacker"
  }
}
```

---

## Observation

The server returned exactly the values that were sent from Burp Repeater.

This confirms that the client controls the HTTP request.

---

## Security Insight

Parameter tampering alone is not a vulnerability.

Applications must validate and authorize every parameter received from the client.

---

## Conclusion

Burp Repeater allows controlled modification of requests, making it an essential tool for manual web application security testing.
