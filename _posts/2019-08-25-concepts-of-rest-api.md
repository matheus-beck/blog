---
layout: post
title: "Concepts of REST API"
date: 2019-08-25 18:21:56 -0300
categories: rest api
---

{% include image.html url="/jekyll-blog/assets/rest-api.png" description="" %}

<style>
.tablelines table, .tablelines td, .tablelines th {
        border: 1px solid black;
        }
</style>

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

| HTTP method | URL              | Route   | Route Parameters | Query Parameters |
| ----------- | -----------------| ------- | ---------------- | ---------------- |
| GET         | http://myapi.com | /users  |                  |   ?page=2        |
| POST        | http://myapi.com | /users  |                  |                  |
| PUT         | http://myapi.com | /users  |       /1         |                  |
| DELETE      | http://myapi.com | /users  |       /1         |                  |
{: .tablelines}

<br>POST and PUT methods can also send a *request body* in their requests. The advantage of this is that request body parameters are not visible in the URL, which makes dealing with sensitive data, like passwords, more secure. An example of a request body would be:
```json
{
    "name": "Matheus",
    "email": "matheus.alencarbeck@gmail.com"
}
```
Another parameter that all HTTP methods described here can use is *Headers*. They are additional data that are not related to the requisition content. Example: It can be used to send authentication like a location.

## HTTP codes

HTTP codes represent the possible states of an HTTP response. They can be:  
  
1xx: Informational  
2xx: Sucess  
&nbsp;&nbsp;&nbsp;&nbsp;200 Sucess  
&nbsp;&nbsp;&nbsp;&nbsp;201 Created  
3xx: Redirection  
&nbsp;&nbsp;&nbsp;&nbsp;301 Moved Permanently  
&nbsp;&nbsp;&nbsp;&nbsp;302 Moved  
4xx: Client Error  
&nbsp;&nbsp;&nbsp;&nbsp;400 Bad request  
&nbsp;&nbsp;&nbsp;&nbsp;401 Unauthorized  
&nbsp;&nbsp;&nbsp;&nbsp;404 Not found  
5xx: Server Error  
&nbsp;&nbsp;&nbsp;&nbsp;500 Internal Server Errors  

<br>Thank you for your time! I hope you have liked this post! :relaxed:

***   
<br>Source: [GoStack Bootcamp from RocketSeat][rocketseat]  


[rocketseat]: https://rocketseat.com.br/
