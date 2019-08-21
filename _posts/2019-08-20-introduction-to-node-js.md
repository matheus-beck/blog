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

The name `npm` means Node Package Manager. It is used to install and manage third party libraries. It also allow us to publish our own libraries.

## What is Yarn?

`Yarn` is also a package manager for Node.js that allow us to do basically everything that `npm` does but `Yarn` has two main advantages:  
<ol>
  <li> It is <strong>faster</strong>. </li>  
  <li> It has functionalities that npm doesn't have. Example: Yarn Workspace. It is used to share dependencies between projects when we're working on multiple projects with the same dependencies in the same folder. </li>   
</ol>  

## Characteristics of Node.js

#### Architecture Event-loop:

This architecture is based on events been registered in the Call Stack. The Call Stack is a stack of events (a function that was triggered by our code) that Node.js process in an eternal loop.

#### Single-Thread

It means it executes in a single thread of our processor. Imagine if we have a processor with four cores. Node.js won't execute at the same time in all cores. All his process will be allocated in a single core. But, Node.js uses a lot of libs from C++, like libuv, that allow us to use multi threads of our processor. So, under the table, the C++ is using the other process threads to process our Call Stack in an faster and more efficient way.

#### Non-blocking I/O

It means that when we make a request to Node.js, like access a page that will return a list, we don't have to return all data from once. Node.js can return this list in parts. It means that when giving a response for the client, Node.js won't block the execution. Using this concept we can have real time applications like a chat. That is, when my front end calls my backend I can maintain an open connection to receive more and more requests.

## ExpressJS

`ExpressJS` is a Node.js framework very good for beginners because it is a micro-framework. That is, small functionalities that play their functions very well. It is very used in micro-services.

<br>Thank you for your time! I hope you have like this post!

***   
Source: [GoStack Bootcamp from RocketSeat][rocketseat]  
[rocketseat]: https://rocketseat.com.br/
