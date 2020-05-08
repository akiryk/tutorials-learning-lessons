# Express

Express is essentially a routing and middleware web framwork. It handles routing on your server and runs middleware in the order you proscribe.

## Instantiate Express

```
const express = require('express');

const app = express();
```

## Controller Functions

```
app.get('/books/:id', function(req, res, next){
  // res.send();
});
```

## Middleware Functions

Format is the same as controller functions, but intent is different. The intent of controllers is to send a response; the intent of middleware is to do something to the request and pass it along.

The order of calls to middleware matters. 
```
// Examples of middleware invoked in order.
app.use(cors());
app.use(json());
app.use(morgan('dev'));
```

Each middleware does something and then calls `next()`, usually without arguments, which are treated as errors.

### Custom middleware example
```
// example custom middleware
const myLogger = (req, res, next) => {
  logRequest(req);
  next();
};

// insert the custom middleware in calls to a specific book
app.get('/book/:id', myLogger, function(req, res, next) {
   //...
})

// multiple middlewares should be passed as an array
app.get('/book/:id', [myLogger, auth, somethingElse], function(req, res, next) {
   //...
})

// Alternatively, 
app.use('/book/:id', function (req, res, next) {
  myLogger(req.method);
  next()
})
```

## Router

Router is an Express class that enables you to make mini-apps within your larger apps. They can have their own authentication, their own middleware, etc. 

```
// instantiate express
const app = express();

// create a new Router
const router = express.Router();

// register (mount) the router, otherwise it won't do anything
// this will use the router miniapp for all routes starting with /me.
app.use('/me', router);
```

Both Router and Express enable you to use the `route` function to streamline.
```
// handle all methods for the route to book
router.route('/book/')
  .get((req, res, next) => { ... })
  .post(...)
  .put(...)
  .delete(...);

// handle all methods for the route to a specific book by id
router.route('/book/:id')
  .get(...)
  // etc.
```
