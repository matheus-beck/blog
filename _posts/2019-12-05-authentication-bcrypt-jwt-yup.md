---
layout: post
title: "Authentication using BCrypt, JWT and YUP"

date: 2019-12-05 18:21:56 -0300
categories: node.js express.js bcrypt jwt yup
---

<h1 align="center">
  <img src="https://vidadeprogramador.com.br/wp-content/uploads/2015/12/tirinha1503.png" width="500">
</h1>

# Password Cryptography using BCrypt

Go to the source folder of your project and run:

```console
yarn add bcryptjs
```

Here, we want to generate a `password_ hash` in our database based on the password typed by the user. This behavior will happen every time you create a new user. The method `bcrypt.hash(user.password, 8);` will create a hash password equivalent to the password of the user and the method `bcrypt.compare(password, this.password_hash);` will return true if the password passed is equal to the hashed password in the database. In your `User.js` model add the following code:

```javascript
import bcrypt from "bcryptjs";
import Sequelize, { Model } from "sequelize";

class User extends Model {
  static init(sequelize) {
    super.init(
      {
        name: Sequelize.STRING,
        email: Sequelize.STRING,
        password: Sequelize.VIRTUAL,
        password_hash: Sequelize.STRING,
        provider: Sequelize.BOOLEAN
      },
      {
        sequelize
      }
    );

    this.addHook("beforeSave", async user => {
      if (user.password) {
        user.password_hash = await bcrypt.hash(user.password, 8);
      }
    });

    checkPassword(password) {
      return bcrypt.compare(password, this.password_hash);
    }

    return this;
  }
}

export default User;
```

# Authentication using JWT and YUP

Go to the source folder of your project and run:

```console
yarn add yup jsonwebtoken
```

You can use `Yup` to validate if the user is passing all the content required in the body of the REST requisition.

You can use `JWT` to authenticate your JSON requisitions. [JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object.](https://jwt.io/introduction/)

Create a `config/auth.js` file with the following (you can use any secret):

```javascript
export default {
  secret: 'A10F8B76D4C3FFC8CF790EE3B6E6AF8E',
  expiresIn: '7d',
};
```

And then in your `SessionController.js` add the following code:

```javascript
import jwt from "jsonwebtoken";
import * as Yup from "yup";
import User from "../models/User";
import authConfig from "../../config/auth";

class SessionController {
  async store(req, res) {
    const schema = Yup.object().shape({
      email: Yup.string()
        .email()
        .required(),
      password: Yup.string().required()
    });

    if (!(await schema.isValid(req.body))) {
      return res.status(400).json({ error: "Validation fails" });
    }

    const { email, password } = req.body;

    const user = await User.findOne({ where: { email } });

    if (!user) {
      return res.status(401).json({ error: "Admin not found" });
    }

    if (!(await user.checkPassword(password))) {
      return res.status(401).json({ error: "Password does not match" });
    }

    const { id, name } = user;

    return res.json({
      user: {
        id,
        name,
        email
      },
      token: jwt.sign({ id }, authConfig.secret, {
        expiresIn: authConfig.expiresIn
      })
    });
  }
}

export default new SessionController();
```

<br>Thank you for your time! I hope you have liked this post! 😊

---

<br>Source: [GoStack Bootcamp from RocketSeat][rocketseat]

[rocketseat]: https://rocketseat.com.br/
