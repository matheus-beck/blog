---
layout: post
title: "Concepts of REST API"
date: 2019-08-25 18:21:56 -0300
categories: rest api
---

{% include image.html url="/blog/assets/rest-api.jpg" description="" %}

## REST API

A REST API is an architecture of development that works as a flux of requests and responses.

## How does it work?

Requisitions, like a browser accessing a URL via ajax (Asynchronous JavaScript and XML), are made by the client. When a request is made to our backend, like a Node.js server, a response is sent through a data structure like a JSON (JavaScript Object Notation). The client receives this data structure and process as he wants.

## Advantages

<ol>
<li> Multiple front-ends using the same back-end </li>
<li> A standardized protocol of communication </li>
</ol>

## Request content of a REST API

A REST API uses routes of communication that uses HTTP methods ( GET, POST, PUT and DELETE).

Examples:

| HTTP method | URL                 | Route Parameters | Query Parameters |
| ----------- | ------------------- | ---------------- | ---------------- |
| GET         | http://minhaapi.com | /users           | ?page=2          |
| POST        | http://minhaapi.com | /users           |                  |
| PUT         | http://minhaapi.com | /users           |                  |
| DELETE      | http://minhaapi.com | /users           |                  |

POST and PUT methods can also send a 'body' of content in the requisition. The advantage of this is that 'body' parameters are not visible in the URL, which makes dealing with sensitive data, like passwords, more secure.

Headers (GET, POST, PUT, DELETE): Additional data that are not related to the requisition content. Send authentication like a location.

## HTTP codes

HTTP codes represent the possible states of an HTTP response. They can be:
1xx: Informational
2xx: Sucess
200 Sucess
201 Created
3xx: Redirection
301 Moved Permanently
302 Moved
4xx: Client Error
400 Bad request
401 Unauthorized
404 Not found
5xx: Server Error
500 Internal Server Errors

---

Thank you for your time! I hope you have liked this post! :relaxed:
