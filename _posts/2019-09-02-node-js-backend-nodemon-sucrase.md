---
layout: post
title: "Node.js Backend using Nodemon and Sucrase"
date: 2019-09-02 18:21:56 -0300
categories: nodemon sucrase node.js express.js
---

{% include image.html url="/blog/assets/node-2.png" description="" %}

## Node.js Backend using Nodemon and Sucrase

In this post, I'm going to show you how to write a simple backend structure and I'm going to present you two development dependencies that will help you a lot.

## File's organization

Create a folder called `backend` and run `yarn init -y` and `yarn add express` inside
that folder. Create a folder inside the `backend` folder called `src`. In `src` we're
going to have our backend structure. Create 3 files inside `src`: `App.js`, `routes.js`
and `server.js` and type the following code:

```javascript
//App.js
import express from "express";
import routes from "./routes";

class App {
  constructor() {
    this.server = express();

    this.middlewares();
    this.routes();
  }

  middlewares() {
    this.server.use(express.json());
  }

  routes() {
    this.server.use(routes);
  }
}

export default new App().server;
```

```javascript
//router.js
import { Router } from "express";

const routes = new Router();

routes.get("/", (req, res) => {
  return res.json({ message: "Hello Beck" });
});

export default routes;
```

```javascript
//server.js
import App from "./App";

App.listen(3000);
```

## Nodemon and Sucrase

These two dependencies will be used while we're developing our backend.
<br>**Nodemon** is a dependency that allows us to re-launch our server every time we change our code, making it easier to develop.
<br>**Sucrase** allows us to use ES6 features in Node.js like the `import` syntax to make our code more legible.

To install these dependencies run inside the `backend` folder:

```console
yarn add nodemon sucrase -D
```

Also, create a file called nodemon.json in the `backend` folder and type the following
to indicate nodemon to launch sucrase-node instead of node when it is executed:

```
{
  "execMap": {
    "js": "sucrase-node"
  }
}

```

In the package.json file, create the following object script as one of the proprieties of the package:

```
"scripts": {
    "dev": "nodemon src/server.js"
  },
```

Now, simple run the server using `yarn dev`.

<br>Thank you for your time! I hope you have liked this post! :smile:

---

<br>Source: [GoStack Bootcamp from RocketSeat][rocketseat]

[rocketseat]: https://rocketseat.com.br/
