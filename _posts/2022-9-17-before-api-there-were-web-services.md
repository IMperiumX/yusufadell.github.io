---

title: Before APIs, there were Web Services
tags: [api]
category: [Web]
layout: post
author:
    name: Yusuf Adel
    link: https://github.com/yusufadell
---

# WEB APIs

> Web **API**  literally sits on top of the existing architecture of the world wide web and relies on a
> host of technologies including HTTP, TCP/IP, and more.

==Ultimately, a web API is a collection of endpoints that expose certain
parts of an underlying database.== As developers we control the URLs for
each endpoint, what underlying data is available, and what actions are
possible via HTTP verbs. By using HTTP headers we can set various
levels of authentication and permission too

## World Wide Web

---

> ###### The Internet is a system of interconnected computer networks that hasexisted since at [least the 1960s](https://en.wikipedia.org/wiki/Internet)

> 1989 when a research scientist at CERN
>
> **Tim Berners-Lee**, invented **HTTP** and ushered in the modern World Wide
> Web. His great insight was that the existing [hypertext system](https://en.wikipedia.org/wiki/Hypertext), where
> text displayed on a computer screen contained links (hyperlinks) to
> other documents, could be moved onto the internet.
> His invention, [Hypertext Transfer Protocol (HTTP)](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol), was the first
> standard, universal way to share documents over the internet.

## URLS

---

> A URL (Uniform Resource Locator) is the address of a resource on the internet.
>
> For example, the Google homepage lives at **<https://www.google.com>.**

* **request and response pattern is the basis of all webcommunication.**
* **client (typically a web browser) requests informatio**n
* **server responds with a response.**

> **<https://python.org/about/>**
>
> **https**, refers to the **scheme** used. it could also be **ftp** for files, **smtp** for email, and so on.
>
> **python.org** is the **host** name
>
> an **(optional) path** - **/about/**

## Internet Protocol Suite

---

> **Once we know the actual URL of a resource, a whole collection of other
> technologies must work properly (together) to connect the client with
> the server and load an actual webpage. This is broadly referred to as the
> internet protocol suite**

**(DNS)** to translate the domain name `google.com` into an `IP address`

> **Domain** names are used because it is
> easier for humans to **remember** a domain name like `google.com` than
> an **IP address** like  `172.217.164.68`.

<u>After the browser has the IP address for a given domain, it needs a way
to set up a consistent connection with the desired server. This happens
via the Transmission Control Protocol (TCP) which provides reliable,
ordered, and error-checked delivery of bytes between two application.</u>

To establish a `TCP` connection between two computers, a three-way `handshake` occurs between the client and server:

* **The client sends a SYN asking to establish a connection**

* **The server responds with a SYN-ACK acknowledging the request and passing a connection parameter**

* **The client sends an ACK back to the server confirming the connection**

## HTTP Verbs

---

> Every webpage contains both an address (the URL) as well as a list of
> approved actions known as HTTP verbs. So far we've mainly talked
> about **getting a web page**, but it’s also possible to **create**, **edit**, and **delete** content

|       CRUD       |   HTTP Versbs   |
| :----------------: | :----------------: |
| **Create** |  **POST**  |
| **Read**<br /> | **GET**<br /> |
| **Update** |  **PUT**  |
| **Delete** | **DELETE** |

---

```ts
To create content you use POST, to read content GET, 
to update it PUT, and to delete it you use DELETE
```

## Endpoints

---

> A traditional website consists of web pages with **HTML, CSS, images,
> JavaScript**, and more. There is a dedicated URL, such as
> example.com/1/, for each page. A web API also relies on URLs and a
> corresponding one might be example.com/api/1/, but **instead** of
> serving up web **pages** consumable by humans it produces **API endpoints**.
> An endpoints contains data, typically in the **JSON** format, and also a list
> of available actions (HTTP verbs).

**GET** returns all users

`https://www.mysite.com/api/users`

 **/api/users**, an available GET request returns list of all available users. This type of endpoint which returns multiple data resources is known as a collection.

###### **GET** returns a single user

`https://www.mysite.com/api/users/<id>`

 **/api/users/<id>**, represents a single user. A
GET request returns information about just that one user.

> If we added a **POST** to the **first** endpoint we could **create a new user**,
> while adding **DELETE** to the **second** endpoint would allow us to delete
> a single user

## HTTP

---

> HTTP is a request-response protocol between two computers that have an
> existing TCP connection.

HTTP Message:

1. **status line**
2. **headers**
3. **optional body data**

---

### Request

```http
GET / HTTP/1.1
Host: google.com
Accept_Language: en-US
```

There are many [HTTP Headers](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields "fuck you") available

### <u>response</u>

```http
HTTP/1.1 200 OK
Date: Mon, 24 Jan 2022 23:26:07 GMT
Server: gws
Accept-Ranges: bytes
Content-Length: 13
Content-Type: text/html; charset=UTF-8
Hello, world!
```

---

## Status Codes

---

> Once your web browser has executed an HTTP Request on a URL there
> is no guarantee things will actually work! Thus there is a quite lengthy
> list of HTTP Status Codes available to accompany each HTTP response.

|  Status Code  |         Means         |
| :-------------: | :----------------------: |
| **2**xx |   **Success**   |
| **3**xx | **Redirection** |
| **4**xx | **Client Error** |
| **5**xx | **Server Error** |

## Statelessness

---

> stateless protocol. This means each request/response pair is completely independent of the previous one
> Statelessness brings a lot of benefits to HTTP. Since all electronic
> communication systems have signal loss over time, if we did not have a
> stateless protocol, things would constantly break if one request/
> response cycle didn’t go through. As a result, HTTP is known as a very
> resilient distributed protocol.
