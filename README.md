# hapi-to-express

This module returns a function that creates mocked Express request and response objects that internally call the Hapi objects passed into the function.

## Usage

### params

**request** - a Hapi request object, ideally within a `'onPostAuth'` server extension point, so that `request.payload` can be read and written to.

**reply** - a Hapi reply object, also hopefully in the `'onPostAuth'` extension point.

### returns
  `{ res: ..., req: ... }` - an object where `res` represents an Express response object and `req` represents an Express request object. Very limited API at the moment.

## Example

```JavaScript
var hapiToExpress = require('hapi-to-express');
var cookieParser = require('cookie-parser');
    
server.ext('onPostAuth', function(request, reply) {
  var hapress = hapiToExpress(request, reply);

  cookieParser()(hapress.req, hapress.res, function(err) {
    if (err) { return reply(err); }
    reply.continue();
  });
});
```

## Note

Currently supporting a limited API based on Hapi 8.\* and Express 4.\* APIs.
