# Practical 3 - Query Parameters

## Objective

Observe how query parameters appear inside an HTTP request.

---

## URL Tested

https://postman-echo.com/get?id=25&name=amna

---

## Intercepted Request

```http
GET /get?id=25&name=amna HTTP/1.1
Host: postman-echo.com
```

---

## Parameters

id=25

name=amna

---

## Observation

The parameters appeared in the first line of the HTTP request after the `?`.

Multiple parameters were separated using `&`.

---

## Conclusion

Query parameters are transmitted to the server as part of the request line.
