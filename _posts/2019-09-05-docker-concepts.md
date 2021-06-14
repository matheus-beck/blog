---
layout: post
title: "Docker Concepts"
date: 2019-09-05 18:21:56 -0300
categories: docker
---

{% include image.html url="/jekyll-blog/assets/docker.png" description="Docker is a tool designed to make it easier to create, deploy, and run applications by using containers - opensource.com :whale:" %}

# What is Docker?

Docker is a platform that help us control the **services** of our application.
Exemple of services: Databases and Email sending.

# How does it work?

It creates **isoleted enviroments**, also know as **containers**.
This containers does not interefeer in the rest of our computer.
Conteriners also exposes **ports** for communication.

# Concepts
<ul>
<li>Image: Service avaiable via Docker. i.e, techs that whe can store in containers.</li>  
<li>Container: Instance of an image. </li>
<li>Docker Registry (Docker Hub): Works similar to npm js </li>  
<li>Dockerfile: "Recepet" of an image </li>
</ul>  
# Dockerfile example

```docker
#Partimos de uma imagem existente
FROM node:10

#Definimos a pasta e copiamos os arquivos
WORKDIR /usr/application
COPY . ./

#Instalamos as dependências
RUN yarn

#Qual porta queremos expor?
EXPOSE 3333

#Executamos nossa aplicação
CMD yarn start
```

<br>Thank you for your time! I hope you have liked this post! :whale:

---

<br>Source: [GoStack Bootcamp from RocketSeat][rocketseat]

[rocketseat]: https://rocketseat.com.br/
