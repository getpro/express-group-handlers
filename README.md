Express Group Handlers
======================

Apply a middleware before or after to a group of route handlers in Express. No need to change your existing code, just call this function (see demos below).

## Install and test
The usual:
```bash
npm install express-group-handlers
npm test
```

## Use
```javascript
var express = require('express')
  , app = express()
  , groupHandlers = require('express-group-handlers');

groupHandlers.setup(app);

app.get('/route1', normalHandler1)
app.get('/route2', normalHandler2)

app.beforeEach(groupHandler, function (app) {
  app.get('/route3', normalHandler3) // GET /route3 will execute groupHandler, then normalHandler3
  app.post('/route4', normalHandler4) // POST /route4 will execute groupHandler, then normalHandler4
  // Note that the syntax is the same than for /route1 and /route2
});

app.listen(3000)
```

The `groupHandlers.setup` function augments your Express app with two functions, `beforeEach` and `afterEach`. Both work the same way: you supply the middlewares you want to see executed before/after the handlers inside the callback. The callback has one parameter, which is a fake Express app with all router functions (`get`, `post`, `all` etc.). If you give it the same name as your real Express app (as in the example above), no need to change your existing code, just wrap the `beforeEach` function around it!

```javascript
// You can have multiple middlewares in beforeEach/afterEach
// You can use arrays of middlewares too
app.beforeEach(gh1, gh2, [gh3, gh4], ..., function (app) {
  // Your routes here
})

// Alternate syntax if you don't want to augment your Express app
// Just don't call groupHandlers.setup and use the functions directly like this
groupHandlers.beforeEach(app, groupHandler, function (app) {
  // Your routes here
});
```




