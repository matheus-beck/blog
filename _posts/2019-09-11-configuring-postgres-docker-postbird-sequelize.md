---
layout: post
title: "PostgreSQL configuration using Docker, Postbird and Sequelize"
date: 2019-09-11 18:21:56 -0300
categories: docker postgresql postbird sequelize
---

{% include image.html url="/blog/assets/postgres-docker.png" description="" %}

_PostgreSQL is a powerful, open source object-relational database system with over 30 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance - https://www.postgresql.org/_

# Configuring PostgreSQL with Docker

Having [Docker](https://docs.docker.com/install/) installed in your machine, go to your terminal and run:

```console
sudo docker run --name database -e POSTGRES_PASSWORD=docker -p 5432:5432 -d postgres
```

then verify your container with the following command:

```console
docker ps
```

Tip: Useful commands you can execute:

```console
docker ps -a : will list all containers in our machine
docker stop database : will stop a docker running process
docker logs database : show log on docker
```

# Visualizing your database with Postbird

Install [PostBird](https://electronjs.org/apps/postbird) in your machine, then go to PostBird and connect to localhost on port 5432 using username = postgres and password = docker (Both defined in the first command executed). After that, create a database with any name you want (In this post we're going to use the name 'gobarber').

{% include image.html url="/blog/assets/postbird.png" description="Test your connection than click on Connect" %}

# Using Sequelize to handle database using Node.js

[Sequelize](https://sequelize.org/) is an ORM that translates JavaScript code to SQL code. The biggest advantage of Sequelize is that it can be used for multiple databases like Postgres, MySQL, MariaDB, SQLite and Microsoft SQL Server.

Run:

```console
yarn add sequelize
yarn add sequelize-cli -D
yarn add pg pg-hstore
```

Create `.sequelizerc` in the source folder and paste:

```javascript
const { resolve } = require("path");

module.exports = {
  config: resolve(__dirname, "src", "config", "database.js"),
  "models-path": resolve(__dirname, "src", "app", "models"),
  "migrations-path": resolve(__dirname, "src", "database", "migrations"),
  "seeders-path": resolve(__dirname, "src", "database", "seeds")
};
```

Also, create `src/config/database.js` and paste:

```javascript
module.exports = {
  dialect: "postgres",
  host: "localhost",
  username: "postgres",
  password: "docker",
  database: "gobarber",
  define: {
    timestamps: true,
    underscored: true,
    underscoredAll: true
  }
};
```

Create an `app` folder to store our models and controllers and a `database` folder with a `migrations` folder inside it.

Now, to generate a model of our migration run:

```console
yarn sequelize migration:create --name=create-users 
```

Edit the created migration in the `src/database/migrations` folder to be like that:

```javascript
module.exports = {
  up: (queryInterface, Sequelize) => {
    return queryInterface.createTable("users", {
      id: {
        type: Sequelize.INTEGER,
        allowNull: false,
        autoIncrement: true,
        primaryKey: true
      },
      name: {
        type: Sequelize.STRING,
        allowNull: false
      },
      email: {
        type: Sequelize.STRING,
        allowNull: false,
        unique: true
      },
      password_hash: {
        type: Sequelize.STRING,
        allowNull: false
      },
      provider: {
        type: Sequelize.BOOLEAN,
        defaultValue: false,
        allowNull: false
      },
      created_at: {
        type: Sequelize.DATE,
        allowNull: false
      },
      updated_at: {
        type: Sequelize.DATE,
        allowNull: false
      }
    });
  },

  down: queryInterface => {
    return queryInterface.dropTable("users");
  }
};
```

After that, to execute the migration:

```console
yarn sequelize db:migrate
```

and to undo the migration (only if necessary):

```console
yarn sequelize db:migrate:undo
```

Now, you can verify the created table in Postbird and the result should look like that:

{% include image.html url="/blog/assets/postbird-migration.png" description="The table 'users' that you have created" %}

<br>Thank you for your time! I hope you have liked this post! :elephant: :whale:

---

<br>Source: [GoStack Bootcamp from RocketSeat][rocketseat]

[rocketseat]: https://rocketseat.com.br/
