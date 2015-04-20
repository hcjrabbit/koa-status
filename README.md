# koa-status


HTTP status utility for node.

## API

```js
var status = require('koa-statuses');
```


If `Integer` or `String` is a valid HTTP code or status message, then the appropriate `code` will be returned. Otherwise, an error will be thrown.

```js
app.status(403) // => 403
app.status('403') // => 403
app.status('forbidden') // => 403
app.status('Forbidden') // => 403
app.status(306) // throws, as it's not supported by node.js
```

### status.codes

Returns an array of all the status codes as `Integer`s.

### var msg = status[code]

Map of `code` to `status message`. `undefined` for invalid `code`s.

```js
app.status[404] // => 'Not Found'
```

### var code = status[msg]

Map of `status message` to `code`. `msg` can either be title-cased or lower-cased. `undefined` for invalid `status message`s.

```js
app.status['not found'] // => 404
app.status['Not Found'] // => 404
```

### status.redirect[code]

Returns `true` if a status code is a valid redirect status.

```js
app.status.redirect[200] // => undefined
app.status.redirect[301] // => true
```

### status.empty[code]

Returns `true` if a status code expects an empty body.

```js
app.status.empty[200] // => undefined
app.status.empty[204] // => true
app.status.empty[304] // => true
```

### status.retry[code]

Returns `true` if you should retry the rest.

```js
app.status.retry[501] // => undefined
app.status.retry[503] // => true
```

### statuses/codes.json

```js
var codes = require('koa-statuses/codes.json');
```

This is a JSON file of the status codes
taken from `require('http').STATUS_CODES`.
This is saved so that codes are consistent even in older node.js versions.
For example, `308` will be added in v0.12.

## Adding Status Codes

The status codes are primarily sourced from http://www.iana.org/assignments/http-status-codes/http-status-codes-1.csv.
Additionally, custom codes are added from http://en.wikipedia.org/wiki/List_of_HTTP_status_codes.
These are added manually in the `lib/*.json` files.
If you would like to add a status code, add it to the appropriate JSON file.

To rebuild `codes.json`, run the following:
