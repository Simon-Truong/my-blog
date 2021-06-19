---
title: "What is a RESTful Api"
date: 2021-05-28T18:24:28+10:00
draft: false
categories: ["architecture", "HTTP"]
---

To understand RESTful, we need to understand the basic concepts of an *API* (Application Programming Interface) and *HTTP* (Hypertext Transfer Protocol).

# API
An API is essentially the middle man between a client and the data they wish to acquire. The API is able to interpret the client's request and handles all the necessary actions such as computation or querying a database, and produces a response that the client consumes.

# HTTP
HTTP is a protocol that the internet uses to enable communication between a *client* and a *server*. Here is an example of a typical workflow:

1. The browser (client) generates a HTTP *request* and sends it to a server
2. The server interprets the client's request, and returns a *response*
3. The browser presents the response in the appropriate manner 

Here is an example of a HTTP request:

```
GET /api/coffee/random_coffee?size=10 HTTP/2
Host: https://random-data-api.com
cookie: session=440e6d7b-b295-43dd-93f8-8c58950c8e0c
```

Let's dive into the anatomy of a HTTP request.

#### HTTP version
`GET /api/coffee/random_coffee?size=10` ***`HTTP/2`***

Specifies which version of HTTP to use. Currently, HTTP/2 is predominantly used throughout the internet.

#### HTTP method
***`GET`*** `/api/coffee/random_coffee?size=10 HTTP/2`

The HTTP method describes what the request is trying to do. In the example, the request is trying to *GET* data. Let's have a look at the HTTP methods we should be aware of (for simplicity, let's consider the context of database records):

- `GET`: a request that is attempting to fetch a record
- `POST`: a request that is attempting to create a new record. Generally, this request is accompanied with a *body*
- `PATCH` & `PUT`: a request that is attempting to update a record. Although similar, a PUT request's body contains the entire record to update so it behaves like a replacement. A PATCH request however, will only contain partial data to update
- `DELETE`: a request that is attempting to delete a record

#### Path
`GET` ***`/api/coffee/random_coffee`***`?size=10 HTTP/2`

#### Host
`Host:` ***`https://random-data-api.com`***

Together, the path and host (base URL) determines the target server to send the HTTP request to. In this case, it will be:

`https://random-data-api.com/api/coffee/random_coffee`

You can get an idea of what the request is trying to achieve by the HTTP method and path. In this example, you can interpret the HTTP request as "GET random coffee".

#### Query Parameters
`GET /api/coffee/random_coffee`***`?size=10`*** `HTTP/2`

Query parameters are key value pairs that provide additional information about the HTTP request. They are delineated by a "*?*", and as seen in this example, we have one query parameter which specifies a size of 10. We can add additional query parameters by appending a "*&*" and the key value pair. For example: 

`?size=10`***`&`***`sort=asc`

#### Headers
***`cookie: session=440e6d7b-b295-43dd-93f8-8c58950c8e0c`***

Headers also provide additional information about the HTTP request. *Cookies* and *Bearer Tokens* are some common header options.

#### Body
A HTTP body usually accompanies a POST or PUT HTTP request, as we need to provide information about the new or replacement record respectively. The type or format of the body is determined by the header `Content-Type`, a common format is *JSON* (Javascript Object Notation). Here is an example:

``` 
{
    "name": "John Doe",
    "address": "101 Foo Bar"
}
```

# RESTful API
RESTful (REpresentational State Transfer) is an architectural design for an API that commonly communicates with the client through HTTP. For an API to be considered RESTful, it must adhere to the following properties:

- `Statelessness`: Each HTTP request is independent from one another, they must not rely on information from prior or subsequent HTTP requests. Individual HTTP request should contain sufficient information to fulfill their purpose and by doing so, minimizes the need for the server to persist sessional data. Ultimately, this designs the API to be more performant and scalable
- `Client-Server Architecture`: The client and the server should be separate from one another, this is also known as *Separation of Concerns*. By keeping the two separate, we enable the individual systems to evolve at their own pace independently, without affecting the other
- `Cacheability`: The response must inform the client whether the response can be cached or not, and if so, for how long. By taking advantage of caching, the client is more performant when the same request is made multiple times
- `Layered System`: The client should not know, nor care, who is receiving it's requests. It should not matter if the request is received by a proxy, a load balancer or the API itself, so long as the client receives the appropriate response. By abstracting away from the details, we are able to implement intermediate layers, such as a load balancer, to improve scalability and performance
- `Uniform Interface`: Communication between the client and API should be standardized. By adhering to this rule, the individual systems can be developed independently without affecting the communication between the two. For example, by agreeing to use the HTTP protocol, the client or server can evolve at their own pace without disturbing current functionality
- `Code on Demand` ***optional***: The server's ability to send executable code to the client