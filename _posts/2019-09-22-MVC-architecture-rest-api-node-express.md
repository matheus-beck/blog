---
layout: post
title: "MVC Architecture in a REST API built with Node.js and Express.js"
date: 2019-09-22 18:21:56 -0300
categories: mvc restapi nodejs expressjs
---

{% include image.html url="/jekyll-blog/assets/mvc.png" description="www.raywenderlich.com" %}

# MVC Architecture

The main purpose to use an MVC architecture is to separate the responsibilities of each type of file in different folders.

# Model:

The models represent abstractions of the database. It is used to manipulate the data in the database tables. They do not contain responsibility for the business rules of our application.

Be sure to have `sequelize` [installed in our project](https://matheus-beck.github.io/blog/docker/postgreesql/postbird/sequelize/2019/09/11/configuring-postgres-docker-postbird-sequelize.html). Now, to create a User model, simply create an `src/app/models` folder and create a `User.js` with the following:

```javascript
import Sequelize, { Model } from "sequelize";

class User extends Model {
  static init(sequelize) {
    super.init(
      {
        name: Sequelize.STRING,
        email: Sequelize.STRING,
        password_hash: Sequelize.STRING,
        provider: Sequelize.BOOLEAN
      },
      {
        sequelize
      }
    );
  }
}

export default User;
```

# Controller

The controllers are the main entrance door of the requisitions of our application. It usually has routers as methods associated with the controllers. They are usually represented as classes that returns a JSON.

**When should I create a new Controller?** Only if I am talking about a different entity that I can represent with only five methods (index, show, store, update, delete).

To create a User Controller, simply create a `src/app/controllers` folder and create a `UserController.js` with the following:

```javascript
import User from "../models/User";

class UserController {
  async store(req, res) {
    const userExists = await User.findOne({ where: { email: req.body.email } });

    if (userExists) {
      return res.status(400).json({ error: "User already exists." });
    }

    const { id, name, email, provider } = await User.create(req.body);

    return res.json({
      id,
      name,
      email,
      provider
    });
  }
}

export default new UserController();
```

# View

The View is the return to the client. In an application, it could be an HTML for example. In this case of a REST API, the View will only be a JSON that will be returned to our front-end and after that, it will be manipulated for ReactJS or React Native for example.

<br>Thank you for your time! I hope you have liked this post! 😇

---

<br>Source: [GoStack Bootcamp from RocketSeat][rocketseat]

[rocketseat]: https://rocketseat.com.br/
