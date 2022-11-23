# Consolidated-U3-Notes

The purpose of this repo is merely to consolidate lesson repos for unit 3 into one repository. 

The consolidation includes content pulled directly from previous repos, elaborations from primary documentation, and rewording for my own benefit and understanding. It excludes follow-along excersizes but links to the original lessons if you need a refresher and want to follow along.

The primary scope of this repo is to serve as a hub/consolidation of lessons from unit 3 but not necessarily as an exhaustive resource for the technology featured.

## Express

[Go to expressjs.com](https://expressjs.com/) to read Official technical documentation for Express.js.

### Express Intro

From [u3_lesson_express_intro](https://github.com/SEIR-1003/u3_lesson_express_intro)

#### What is Express.js?

Express is a JS library to set up your own server, which listens for different kinds of HTTP requests, and serves the right response.

In our case, we're using it solely as a JSON API server.

#### HTTP

HTTP is the structure of messages that all information travels in over the web. When you visit a webpage you are making an HTTP request.

The HTTP request and response cycle is at the heart of the web.


#### Getting Started

##### Installation

Install express at the root level of your backend project through your terminal with `npm install express`.

##### Boilerplate

To use express, we need to set up a server filer in the root directory of our backend project and include the following boilder plate code. I've added comments from the Express technical documentation to elaborate peices of code and their function.

```
const express = require('express')
const PORT = process.env.PORT || 3001

// The app object conventionally denotes the Express application. Create it by calling the top-level express() function exported by the Express module:
const app = express()


//Starts a UNIX socket and listens for connections on the given path. This method is identical to Node’s http.Server.listen().
app.listen(PORT, () => {
  console.log(`Express server listening on port ${PORT}`)
})
```

In short, we require the package in our file, declare our app object and assign it to the imported express function, and select a port to "listen" to for HTTP requests.

##### Installing and using nodemon

You could run your server with the command `node [serverFileName].js`. This would spin up your server once but the downside is that you'll have to stop and restart your server after every change while you're developing.

The package `nodemon` enables you to make changes live so that you don't have to stop and restart the server after every change you make. This needs to be installed on a project-to-project basis with the command `npm install nodemon --save-dev`.

You may have to manually update the "scripts" attribute in your package.json folder to add a start script and dev script. Add these properties to your json as they're written below.

```
"scripts": {
  "start": "node server.js",
  "dev": "nodemon server.js"  
}
```

You can start your live server with the `npm run dev` command in your terminal.


### Express Routes

From [u3_lesson_express_routing](https://github.com/SEIR-1003/u3_lesson_express_routing)

In Express.js, routes are paths the user makes an HTTP for, such as GET `/` GET `/news` and so on. Upon making a request to a particular path, a handler function takes care of that particular request to create, update, read, or destroy information on a database.

#### Building Routes and Handlers/Controllers

Each HTTP request function (`get`, `post`, `put`, `delete`, etc) require two arguments. The first is a string representing the `url` or `endpoint` that we want to make the request to. The second argument is a function that provides a way to handle the specific request.

This second argument, the handler function, works with two parameters: `req` and `res`.

The `req` parameter conventionally represents the request being made and any information sent alongside the request. [Read about req](https://expressjs.com/en/api.html#req) in the Expressjs documentation.

The `res` variable respresents the HTTP response from the server. [Read about res](https://expressjs.com/en/api.html#res) in the Expressjs documentation.

#### Dynamic Endpoints

The `request` object enables you to declare dynamic endpoints using parameters and queries.

##### req.params

Dynamic parameters can be appended to paths with a colon. These parameters can be named however you'd like but its worth considering semantic conventions.

```
app.get('/message/:id', (request, response) => {
  console.log(`Getting a message with the id of ${request.params.id}`)
  response.send({ msg: `Message with an id of ${request.params.id} found` })
})
```

##### req.query

Similarly, queries can be appended to the path with a question mark. Multiple queries are separated by ampersands. Example below:

```
localhost:3001/find?myName=Bob&myAge=23
```

Our path and handler function might look like this:

```
app.get('/find', (request, response) => {
  console.log(
    `Finding someone with a name of ${request.query.myName} and an age of ${request.query.myAge}`
  )
  response.send({
    msg: `${request.query.myName} is ${request.query.myAge} years old.`
  })
})
```

Query's function in different way from `params` because we dont set any placeholders ahead of time. Instead this information is given when constructing the endpoint:

### Express Middleware

From [u3_lesson_express_middleware](https://github.com/SEIR-1003/u3_lesson_express_middleware)

### Express Controllers

From [u3_lesson_express_controllers](https://github.com/SEIR-1003/u3_lesson_express_controllers)