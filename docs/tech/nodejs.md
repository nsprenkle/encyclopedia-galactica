## NodeJS
Node has an event loop (async!)

Since the code is async we have to think about how we write differently:

``` javascript
// Old style
var connection = getDbConnection(connectionString);
var statement = connection.createStatement();…

// Async - callbacks w/ event emitters
getDbConnection(connectionString, function(err, conn) {
  conn.createStatement(function …
  }
}
```

Conventions:
  1. Callbacks are last parameter in an async function call
  2. Error is first parameter to callback function
  3. Check that error is undefined to continue

https://www.w3schools.com/nodejs/nodejs_get_started.asp