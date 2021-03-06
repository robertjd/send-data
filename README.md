# send-data [![build status][1]][2]

send data through response

## Example

```js
var send = require("send-data")
var sendJson = require("send-data/json")
var sendHtml = require("send-data/html")
var sendError = require("send-data/error")
var http = require("http")

http.createServer(function handleRequest(req, res) {
    if (req.url === "/send") {
        send(req, res, {
            body: "foo",
            statusCode: 202,
            headers: {
                bar: "baz"
            }
        })
    } else if (req.url === "/optional") {
        send(req, res, "foo")
    } else if (req.url === "/json") {
        sendJson(req, res, {
            body: {
                foo: "bar"
            },
            statusCode: 201
        })
    } else if (req.url === "/json/optional") {
        sendJson(req, res, {
            foo: "bar"
        })
    } else if (req.url === "/html") {
        sendHtml(req, res, {
            body: "<div>foo</div>",
            statusCode: 200,
            headers: {}
        })
    } else if (req.url === "/html/optional") {
        sendHtml(req, res, "<div>foo</div>")
    } else if (req.url === "/oops") {
        sendError(req, res, new Error("OOPS"))
    }
}).listen(8080)
```

## Docs

```ocaml
send-data := (HttpRequest, HttpResponse, Buffer | String | {
    headers?: Object<String, String>,
    body?: Buffer | String,
    statusCode?: Number
})

send-data/json := (HttpRequest, HttpResponse, Value | {
    body: Value,
    headers?: Object<String, String>,
    statusCode?: Number
})

send-data/html := (HttpRequest, HttpResponse, String | {
    body: String,
    headers?: Object<String, String>,
    statusCode?: Number
})

type ErrorObject := { attribute: String, message: String }
type MaybeErrorObject := Array<ErrorObject> | String | Error

send-data/error := (HttpRequest, HttpResponse, MaybeErrorObject | {
    body: MaybeErrorObject,
    statusCode?: Number,
    headers?: Object<String, String>
})
```

## Installation

`npm install send-data`

## Tests

`npm test`

## Contributors

 - Raynos

## MIT Licenced

  [1]: https://secure.travis-ci.org/Raynos/send-data.png
  [2]: http://travis-ci.org/Raynos/send-data
