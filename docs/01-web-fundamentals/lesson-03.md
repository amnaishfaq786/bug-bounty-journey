# Lesson 03 – HTTP Methods



## Objective



By the end of this lesson, you will understand:



- What HTTP methods are.

- Why different HTTP methods exist.

- The difference between GET and POST.

- The structure of an HTTP request.

- The purpose of Content-Type and Content-Length.

- Why HTTP methods matter in web security.



---



# Prerequisites



Before starting this lesson, you should have completed:



- Lesson 01 – HTTPS Request Anatomy

- Lesson 02 – Browser HTTP Requests

- Burp Suite installed and configured

- Browser traffic successfully intercepted



---



# Introduction



When a browser communicates with a web server, it doesn't simply ask for a webpage. It also tells the server **what action it wants to perform**.



This action is called the **HTTP Method**.



Think of an HTTP method as a verb in a sentence.



For example:



```

GET /products

```



means:



> "Retrieve the products."



While:



```

POST /login

```



means:



> "Process the login information I'm sending."



The URL tells the server **which resource** we want.



The HTTP method tells the server **what we want to do** with that resource.



---



# Why Do HTTP Methods Exist?



Imagine if every request looked like this:



```

GET /something

```



How would the server know whether you wanted to:



- View your profile

- Update your profile

- Delete your profile

- Create a new account



It couldn't.



HTTP methods solve this problem by communicating the intent of the request.



---



# Real-World Analogy



Imagine visiting a library.



Different actions require different requests.



| Library Action | HTTP Method |

|----------------|------------|

| Read a book | GET |

| Submit a membership form | POST |

| Replace your address | PUT |

| Update only one detail | PATCH |

| Cancel your membership | DELETE |



The librarian needs to know **what you want to do**, not just **which book** you are referring to.



HTTP methods work the same way.



---



# GET Method



GET is used to **retrieve information** from the server.



Example:



```

GET /products

```



The server responds with the requested data.



GET requests should **not change data** on the server.



Examples:



- Viewing a webpage

- Opening an image

- Reading API data

- Downloading a PDF



---



# POST Method



POST is used to **send data** to the server.



Unlike GET, POST usually contains a **request body**.



Example:



```

POST /login



username=john

password=secret

```



The server processes the submitted data.



Common uses:



- Login forms

- Registration forms

- Contact forms

- File uploads

- API requests



---



# GET vs POST



| Feature | GET | POST |

|---------|-----|------|

| Purpose | Retrieve data | Submit data |

| Request Body | No | Yes |

| Changes Server Data | Should not | Usually does |

| Common Usage | Reading resources | Form submission |



---



# HTTP Request Structure



A typical HTTP request consists of four parts.



```

Request Line



Headers



Blank Line



Body

```



Example:



```

POST /post HTTP/1.1

Host: httpbin.org

Content-Type: application/x-www-form-urlencoded

Content-Length: 15



name=test&age=1

```



---



# Content-Type



The Content-Type header tells the server what type of data is being sent.



Example:



```

Content-Type: application/x-www-form-urlencoded

```



This tells the server that the request body contains form data.



Example body:



```

name=test&age=1

```



---



# Content-Length



Content-Length tells the server how many bytes exist in the request body.



Example:



```

Content-Length: 15

```



The server reads exactly this many bytes before processing the request.



---



# Practical Exercise



Using Burp Suite Repeater:



Original request:



```

GET /get HTTP/1.1

```



Modified request:



```

POST /post HTTP/1.1

Host: httpbin.org

Content-Type: application/x-www-form-urlencoded

Content-Length: 15



name=test&age=1

```



The server successfully processed the request and returned:



```

{

  "form": {

    "name": "test",

    "age": "1"

  }

}

```



This demonstrates how POST sends data inside the request body.



---



# Security Perspective



Using the correct HTTP method is important.



For example:



```

GET /delete-account?id=123

```



would allow an attacker to trick a logged-in user into visiting a malicious link.



Since GET requests should only retrieve information, sensitive actions like deleting accounts should use methods such as POST or DELETE together with proper protections like CSRF tokens and authorization checks.



Bug bounty hunters often test whether applications misuse HTTP methods because incorrect implementations can introduce security vulnerabilities.



---



# Key Takeaways



- HTTP methods describe the action the client wants to perform.

- The URL identifies the resource.

- GET retrieves data.

- POST submits data.

- POST requests usually contain a request body.

- Content-Type describes the body format.

- Content-Length specifies the body size.

- Choosing the correct HTTP method improves both application design and security.



---







# Summary



HTTP methods define the action a client wants to perform on a resource. GET retrieves information, while POST submits data for processing. By intercepting and modifying requests with Burp Suite, we observed how request methods, headers, and bodies work together. Understanding HTTP methods is a fundamental skill for both web development and web security because many vulnerabilities arise from incorrect handling of these methods.
