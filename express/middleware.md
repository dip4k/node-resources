# List of middlewares

* [Expressa](https://github.com/thomas4019/expressa) - express middleware for easily making REST apis.
* [morgan](https://github.com/expressjs/morgan) - for logging each request.
* [cors](https://github.com/expressjs/cors) - enable CORS support.
* [body-parser](https://github.com/expressjs/body-parser) - node.js body parsing middleware.
* [multer](https://github.com/expressjs/multer) - node.js middleware for handling multipart/form-data.
* [busboy](https://www.npmjs.com/package/busboy) - for handling multipart/form-data.
* [formidable](https://www.npmjs.com/package/formidable)- for handling multipart/form-data.
* [session](https://github.com/expressjs/session) - simple session middleware for Express.
* [errorhandler](https://github.com/expressjs/errorhandler) - development-only error handler middleware.
* [serve-favicon](https://github.com/expressjs/serve-favicon) - favicon serving middleware.
* [csurf](https://github.com/expressjs/csurf) - node.js CSRF protection middleware.
* [Passport](http://www.passportjs.org/) - Simple, unobtrusive authentication.
* [Merror](https://github.com/mamsoudi/merror) - A RESTful-friendly Express Middleware for HTTP error handling and error responses.

## Usage

1. For serving static folders

   ```javascript
   app.use(express.static('client'));
   ```

2. For parsing request body

   ```javascript
   app.use(bodyParser.urlencoded({ extended: true }));
   app.use(bodyParser.json());
   ```

3. For Enabling cors

   ```javascript
   app.use(
     cors({
       origin: ['http://localhost:3001'],
       methods: ['GET', 'POST'],
       allowedHeaders: ['Content-Type', 'Authorization']
     })
   );
   ```

4. For Logging

   ```javascript
   app.use(morgan('common'));
   ```

5. Compacting requests using GZIP middleware

   ```javascript
   app.use(compression('npm install compression--save '));
   ```

6. Enabling security middleware that handles several kinds of attacks in the HTTP/HTTPS protocols. This module is called helmet which is a set of nine internal middlewares,
   ```javascript
   app.use(helmet('npm install helmet--save'));
   ```

### Example of Using middleware

```javascript
var express = require('express');
var cors = require('cors');
var morgan = require('morgan');
var compression = require('compression');
var fs = require('fs');
var https = require('https');
var helmet = require('helmet');
var app = express();
app.use(morgan('common'));
app.use(helmet());
app.use(
  cors({
    origin: ['http://localhost:3001'],
    methods: ['GET', 'POST'],
    allowedHeaders: ['Content-Type', 'Authorization']
  })
);
app.use(compression());
app.get('/', function(req, res) {
  res.json({
    status: 'My API is alive!'
  });
});

//optional for providing ssl certificates
var credentials = {
  key: fs.readFileSync('my-api.key', 'utf8'),
  cert: fs.readFileSync('my-api.cert', 'utf8')
};
https.createServer(credentials, app).listen(3000, function() {
  console.log('My API is running...');
});
```

### References

> [express-middleware-guide](https://expressjs.com/en/guide/using-middleware.html)

> [express-middleware-resources](https://expressjs.com/en/resources/middleware.html)
