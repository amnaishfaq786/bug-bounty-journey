# Practical 2 - Fragment Test

## Objective

Verify whether URL fragments are transmitted to the server.

---

## URL Tested

https://httpbin.org/get#myfragment

---

## Intercepted Request

```http
GET /get HTTP/1.1
Host: httpbin.org
```

---

## Observation

The browser removed:

#myfragment

before sending the request.

The fragment never appeared inside Burp Suite.

---

## Conclusion

Fragments are handled entirely by the browser and are not transmitted to the web server.
