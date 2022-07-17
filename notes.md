# Section 2. A mini-microservices app

## App Overview

![img.png](images-notes/app-overview-1.png)

## Project Setup
![img.png](images-notes/project-setup-1.png)

Initial app setup:
- generate react app using create-react-app  
- create express-based project for the posts service
- crete express-based project for the comments service 

`mkdir blog & cd blog`  

client folder:  
`npx create-react-app client`  

posts folder:  
`mkdir posts & cd posts`  
`npm init -y`  
`npm i express cors axios nodemon`  

comments folder:  
`mkdir posts & cd posts`  
`npm init -y`  
`npm i express cors axios nodemon`  

## Posts Service Creation
Methods:
- get
- post - create new post

## Implementing a Comments Service
![img.png](images-notes/ .png)
![img.png](images-notes/comments-service-2.png)


```js
const express = require('express');
const bodyParser = require("body-parser")
const {randomBytes} =require("crypto");

const app = express();
app.use(bodyParser.json())

const commentsByPostId = {};

app.get('/posts/:id/comments', (req, res) => {
  res.send(commentsByPostId[req.params.id] || []);
})

app.post('/posts/:id/comments', (req, res) => {
  const commentId = randomBytes(4).toString('hex');
  const {content} = req.body;
  const comments = commentsByPostId[req.params.id] || [];
  comments.push({id: commentId, content})
  commentsByPostId[req.params.id] = comments;
  res.status(201).send(comments);
})

app.listen(4001, () => {
  console.log("Listening on 4000")
})
```
