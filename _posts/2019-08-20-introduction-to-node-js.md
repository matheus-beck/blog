---
layout: post
title: "Introduction to Node.js"
date: 2019-08-20 18:21:56 -0300
categories: node.js
---

{% include image.html url="/blog/assets/node.png" description="" %}

## What is Node.js?

Node.js is a platform that allow us to use JavaScript in the backend. It is built on V8 (Google Chrome's motor written in C++).

## What is npm?

The name `npm` means Node Package Manager. It is used to install and manage third party libraries. It also allows us to publish our own libraries.

## What is Yarn?

`Yarn` is also a package manager for Node.js that allows us to do basically everything that `npm` does but `Yarn` has two main advantages:  
<ol>
  <li> It is <strong>faster</strong>. </li>  
  <li> It has functionalities that npm doesn't have. Example: Yarn Workspace. It is used to share dependencies between projects when we're working on multiple projects with the same dependencies in the same folder. </li>   
</ol>  

## Characteristics of Node.js

#### Architecture Event-loop:

This architecture is based on events been registered in the Call Stack. The Call Stack is a stack of events (a function that was triggered by our code) that Node.js process in an eternal loop.

#### Single-Thread

It means it executes in a single thread of our processor. Imagine if we have a processor with four cores. Node.js won't execute at the same time in all cores. All his process will be allocated in a single core. But, Node.js uses a lot of libs from C++, like libuv, that allow us to use multi threads of our processor. So, under the table, the C++ is using the other process threads to process our Call Stack in a faster and more efficient way.

#### Non-blocking I/O

It means that when we make a request to Node.js, like access a page that will return a list, we don't have to return all data from once. Node.js can return this list in parts. It means that when giving a response to the client, Node.js won't block the execution. Using this concept we can have real time applications like a chat. That is, when my front end calls my backend I can maintain an open connection to receive more and more requests.

## ExpressJS

`ExpressJS` is a Node.js framework very good for beginners because it allows us to create REST APIs faster and in a simple way. It is a micro-framework, i.e. small functionalities that play their functions very well. And it is very used in micro-services.

## Hello Node.js

Create a folder called `hello-node` and execute the following command inside that folder:  
```console
yarn init -y
```
This command will initiate our project creating a file called `package.json`. This file will save all the references to the dependencies that we're going to use (like Express.js). 

Also, inside that folder, execute the command:
```console
yarn add express 
```
This command will install Express.js as our dependency. Realize that now we have a `node_modules` folder containing the source code of Express.js and all the dependencies that Express.js uses.

Now, create a file called `index.js` and type:

```javascript
const express = require('express');

const server = express();

server.get('/', (req, res) => {
    return res.json({ message: 'Hello Node' });
    
});

server.listen(3000);
```

Now, if we run the command 
```console
node index.js
````
and access http://localhost:3000/ in our browser we'll see that Node.js returned us an object like { "message":"Hello Node" }.

We could have use ```return res.send('Hello World');``` to return a string, but it is a best practice in the development of a REST API to always make our backend return a JSON.


<br>Thank you for your time! I hope you have liked this post! :smile:

***   
<br>Source: [GoStack Bootcamp from RocketSeat][rocketseat]  


[rocketseat]: https://rocketseat.com.br/
