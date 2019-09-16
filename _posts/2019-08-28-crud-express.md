---
layout: post
title: "CRUD using Express.js middleware"
date: 2019-08-28 18:21:56 -0300
categories: crud node.js express.js
---

{% include image.html url="/blog/assets/crud.png" description="" %}

## CRUD

CRUD means CREATE, READ, UPDATE and DELETE. In this article, we're going to create these four functions, in an Express.js server, to handle a simple local array (This array will represent our database)

## Server structure

Create a folder called `src` and run the commands `yarn init -y` and `yarn add express` inside that folder. Create a file `index.js` with the structure of our server:

```javascript
const express = require("express");

const server = express();

server.use(express.json()); // Read JSON from req.body

const users = ["Paul", "George", "John", "Ringo"];

/*
  All CRUD functions will be here
*/

server.listen(3000);
```

## Create

To add a new user to our array, we're going to use a `POST` method and pass the name of the user through the body of our requisition. Add the following function to your code:

```javascript
server.post("/users", (req, res) => {
  const { name } = req.body;

  users.push(name);

  return res.json(users);
});
```

## Read

To read the users we're going to use the `GET` method in two ways. One to read a specific user and the other to list all users in the array. Add the following functions to your code:

```javascript
server.get("/users", (req, res) => {
  return res.json(users);
});

server.get("/users/:index", (req, res) => {
  return res.json(users[req.params.id]);
});
```

## Update

To update a user, we're going to use the `PUT` method:

```javascript
server.put("/users/:index", (req, res) => {
  const { name } = req.body;
  const { index } = req.params;

  users[index] = name;

  return res.json(users);
});
```

## Delete

Finally, to delete a user from our array we're going to use the `DELETE` method:

```javascript
server.delete("/users/:index", (req, res) => {
  const { index } = req.params;

  users.splice(index, 1);

  return res.send();
});
```

## Middleware

A middleware is a function that receives a requisition and response and process that data.
Every function described here in the format (req, res) => {/** Do stuff **/} is a middleware.
In Express.js, we can call one or more middleware in our requisitions.

Here, we're going to define a global middleware that is going to be called before every other middleware. It will calculate the time of every requisition and print the method and the URL that is being called. The `next` parameter is necessary to call for the next middleware of our server instead of stopping the execution of the server:

```javascript
server.use((req, res, next) => {
  console.time("Request");
  console.log(`METHOD: ${req.method}; URL: ${req.url}`);

  next();

  console.timeEnd("Request");
});
```

Create this two other middleware to check for errors in our calls to the server and add then to our CRUD methods:

```javascript
function checkUserExists(req, res, next) {
  if (!req.body.name) {
    return res.status(400).json({ error: "User name is required" });
  }

  return next();
}

function checkUserInArray(req, res, next) {
  const user = users[req.params.index];

  if (!user) {
    return res.status(400).json({ error: "User does not exists" });
  }

  req.user = user;

  return next();
}

server.get("/users", (req, res) => {
  /* Same code ... */
});

server.get("/users/:index", checkUserInArray, (req, res) => {
  /* Same code ... */
});

server.post("/users", checkUserExists, (req, res) => {
  /* Same code ... */
});

server.put("/users/:index", checkUserExists, checkUserInArray, (req, res) => {
  /* Same code ... */
});

server.delete("/users/:index", checkUserInArray, (req, res) => {
  /* Same code ... */
});
```
## API Calls:
To test our server, use a REST client like [Insomnia][insomnia]:

#### CREATE USER:

{% include image.html url="/blog/assets/post.png" description="Create user example" %}

#### READ USER:

{% include image.html url="/blog/assets/get-all.png" description="Read all users example" %}

{% include image.html url="/blog/assets/get-id.png" description="Read user by id example" %}

#### UPDATE USER:

{% include image.html url="/blog/assets/update.png" description="Update user example" %}

#### DELETE USER:

{% include image.html url="/blog/assets/delete.png" description="Delete user example" %}
{% include image.html url="/blog/assets/after-delete.png" description="List after delete" %}

You can check the complete code in this repo: [https://github.com/matheus-beck/users-manager/][https://github.com/matheus-beck/users-manager/]

<br>Thank you for your time! I hope you have liked this post! :smile:

---

<br>Source: [GoStack Bootcamp from RocketSeat][rocketseat]

[rocketseat]: https://rocketseat.com.br/
[insomnia]: https://insomnia.rest/
[https://github.com/matheus-beck/crud-express/]: https://github.com/matheus-beck/crud-express/
