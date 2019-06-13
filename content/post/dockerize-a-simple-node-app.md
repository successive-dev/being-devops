---
title: "Dockerize a Simple Node App"
date: 2019-06-07T10:17:45+05:30
draft: false
tags: ["docker","container","node","app"]
---
Today, I am gonna show you how to dockerize a node.js application. Firstly I am going to create a basic node app and then write the Dockerfile to create the image of the application.

### First, lets create a simple node.js application

So you can quicky setup a very simple helloWorld node app by running following commands in terminal.
    
```shell 
$ git clone https://github.com/successive-dev/nodejs_helloworld.git
$ cd nodejs_helloworld
$ node helloworld.js
```

Head over to [localhost:3000](http://localhost:3000) in your browser to check if its working.

### Creating a Dockerfile

Dockerfile is a layout of image. It tells what things to go inside an image etc. The below Dockerfile is a very simple one. Let me explain what it is doing at each step.

```Dockerfile
FROM node:current-alpine

# It's pulling an image named node:current-alpine, which is nothing but node environment on top of an OS, which in this case is Alpine Linux. So till this point you can think that we have an OS with node installed.

WORKDIR /app

# It's just setting up a working directory.

COPY package.json /app
COPY helloworld.js /app

# Copying the files necessary to have the app running in the container

RUN npm i

# Installing dependencies

CMD [ "node", "helloworld.js" ]

# Setting up the entry point, this command will execute when container is created and is running
```

### Build and Run the image

Run the following commands to build image and run it.
```bash 
$ docker build -t helloworld . # docker build -t [image_name] [path_to_Dockerfile] : to build image
$ docker run -d -p 3000:3000 helloworld # docker run -d -p [host_machine_port:container_port] [image_name]
```
Go to [localhost:3000](http://localhost:3000) in your browser and you should see Hello World! message.
