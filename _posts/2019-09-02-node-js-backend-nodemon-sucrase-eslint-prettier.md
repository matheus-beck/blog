---
layout: post
title: "Node.js Backend using Nodemon, Sucrase, ESLint and Prettier"
date: 2019-09-02 18:21:56 -0300
categories: nodemon sucrase eslint prettier node.js express.js
---

{% include image.html url="/blog/assets/node-2.png" description="" %}

## Node.js Backend using Nodemon, Sucrase, ESLint and Prettier

In this post, I'm going to show you how to write a simple backend structure and I'm going to present you four development dependencies that will help you a lot.

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

## Dev Dependencies
Nodemon, Sucrase, ESLint and Prettier. These four dependencies will be used while we're developing our backend.

To install these dependencies run inside the `backend` folder:

```console
yarn add nodemon sucrase eslint prettier eslint-config-prettier eslint-plugin-prettier -D
```
## Nodemon and Sucrase
<br>**Nodemon** is a dependency that allows us to re-launch our server every time we change our code, making it easier to develop.
<br>**Sucrase** allows us to use ES6 features in Node.js like the `import` syntax to make our code more legible.

To configure these dependencies, create a file called nodemon.json in the `backend` folder and type the following to indicate nodemon to launch sucrase-node instead of node when it is executed:

```
{
  "execMap": {
    "js": "sucrase-node"
  }
}

```

Now, in the package.json file, create the following object script as one of the proprieties of the package:

```
"scripts": {
    "dev": "nodemon src/server.js"
  },
```

## ESLint and Prettier
<br>**ESLint** verifies if the code is following the established patterns.
<br>**Prettier** verify code patterns like the size of the code line.

First, install the [ESLint extension for VSCode](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint).  
Then, execute `yarn eslint --init` and use the following config:  
{% include image.html url="/blog/assets/eslint-config.png" description="" %}  

After that, remove the package-lock.json file if you're only using yarn. 

Also, run `yarn` in the project folder after installing all dependencies to map the newly installed dependencies in `yarn.lock`. Now, add the following to your `settings.json` file in vscode:

```
"eslint.autoFixOnSave": true
"eslint.validate": [
    {
      "language": "javascript",
      "autoFix": true
    },
]
```

to auto-correct on saving.

Also, add the following to your `.eslintrc.js` generated file to override some rules that may interfere in our backend development (feel free to add or remove any rule you like):

```
rules: {
    "prettier/prettier": "error",
    "class-methods-use-this":"off",
    "no-param-reassign": "off",
    "camelcase": "off",
    "no-unused-vars":["error",{ "argsIgnorePattern": "next" }]
  },
```

And add the following to use prettier in the same `.eslintrc.js` file:

```
  extends: ["airbnb-base", "prettier"],
  plugins: ["prettier"],
```

Finally, create a `.prettierrc` file in the source folder with the following:

```
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

Now, simple run the server using `yarn dev`.

Tip: You can use the command `yarn eslint --fix src --ext .js` to apply an auto fix
in all the contents of our folder `src`.

<br>Thank you for your time! I hope you have liked this post! :smile:

---

<br>Source: [GoStack Bootcamp from RocketSeat][rocketseat]

[rocketseat]: https://rocketseat.com.br/
