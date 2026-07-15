# Lesson 02 – Browser HTTP Requests

---

# Objective

In this lesson we will learn:

- How a browser communicates with a web server.
- Why browsers send much more information than curl.
- How Burp Suite intercepts requests.
- Why every piece of client data can be modified.
- Why servers should never trust client input.

---

# Prerequisites

Before this lesson you should understand:

- What HTTP is
- Client vs Server
- Basic GET requests
- Using curl

---

# Introduction

During the previous lesson we created a request using curl.

That request contained only a few headers because curl is a command-line HTTP client.

A real web browser is much more complex.

It tells the server:

- what browser it is
- which operating system it is running
- which language the user prefers
- which file formats it understands
- which compression methods it supports
- whether this navigation came from another website
- many other browser capabilities

This information is sent using **HTTP Headers**.

---

# Real World Analogy

Imagine you order food online.

The restaurant first needs to know:

Who are you?

What language do you speak?

Where should the food be delivered?

What payment methods do you support?

Do you have allergies?

The order itself may simply be:

"I want one pizza."

But the extra information helps the restaurant provide a better experience.

HTTP works exactly the same way.

The URL is the order.

The headers describe the customer.

---

# Browser Request

The browser sent the following request.

```http
GET / HTTP/1.1
Host: example.com
Sec-Ch-Ua: "Not-A.Brand";v="24", "Chromium";v="146"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Accept-Language: fr
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/146.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
Connection: keep-alive
```

---

# Understanding Each Header

## GET

```http
GET /
```

GET asks the server to return a resource.

No data is uploaded.

---

## Host

```http
Host: example.com
```

Tells the web server which website is being requested.

A single server can host hundreds of websites.

---

## User-Agent

```http
User-Agent: Mozilla/5.0...
```

Identifies:

- Browser
- Operating System
- Rendering Engine

Many websites customize content based on this value.

---

## Accept

```http
Accept:
```

Lists the content types the browser can display.

Examples include:

- HTML
- XML
- Images
- Other web content

---

## Accept-Language

```http
Accept-Language: fr
```

The browser requests French content.

The server may:

- Return French
- Ignore the request
- Return English

The decision belongs to the server.

---

## Accept-Encoding

```http
Accept-Encoding: gzip, deflate, br
```

The browser tells the server it supports compressed responses.

Compression makes websites load faster.

---

## Sec-Fetch Headers

Examples:

```
Sec-Fetch-Site
Sec-Fetch-Mode
Sec-Fetch-User
Sec-Fetch-Dest
```

These modern browser headers help servers understand:

- Where the request originated
- Whether it came from another website
- Whether it was user initiated
- What resource is being requested

They improve browser security.

---

# Practical Lab

Tool Used:

Burp Suite Community Edition

Target:

https://example.com

Procedure:

1. Started Burp Suite.
2. Opened Burp Browser.
3. Enabled Intercept.
4. Visited example.com.
5. Burp intercepted the request.
6. Changed

Accept-Language

from

en-US

to

fr

7. Forwarded the request.
8. Observed the server response.

---

# Observation

Although the browser requested French,

the server still returned the page in English.

Reason:

The server decides whether to honor client preferences.

The client can request.

The server decides.

---

# Security Importance

This lesson teaches one of the most important principles in cybersecurity.

Every request sent by the client can be modified.

Attackers can modify:

- Headers
- Cookies
- Parameters
- Hidden Fields
- Request Body
- HTTP Method

Because of this,

servers must never trust client data.

Always validate everything on the server side.

---

# Key Takeaways

✔ Browsers send much more information than curl.

✔ HTTP Headers describe the client.

✔ Burp Suite can intercept requests.

✔ Requests can be modified before reaching the server.

✔ The server makes the final decision.

✔ Never trust client-side input.

---

# Reflection

Question:

Does a browser send exactly the same request as curl?

Answer:

No.

A browser sends many additional headers that help servers understand the client's capabilities, preferences, browser type, operating system and security context.

Question:

Why did changing Accept-Language not translate the page?

Answer:

Because the server ignored the preference and returned its default language.

Question:

What is the biggest lesson from this lab?

Answer:

The client controls the request.

The server controls the response.

