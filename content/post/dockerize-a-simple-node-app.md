---
title: "Dockerize a Simple Node App"
date: 2019-06-07T10:17:45+05:30
draft: true
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

Head over to `localhost:3000` in your browser to check if its working.

