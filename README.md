# ShortyResty
ShortyResty is a Golang REST API service that shortens URLs and allows the user to redirect to their shortened URL

## Usage
To shorten a URL:
1. Send a POST request to "http://127.0.0.1:8080/shorten"
2. Request should be in JSON with the format {"url": "http://example.com/verylonguselessURLthatdoesnotseemtoend/123"}
3. Response will be in JSON with the format {"short_url": "127.0.0.1:8080/xxxxxxxx"}

To redirect from a shortened URL:
1. Send a GET request to "http://127.0.0.1:8080/$ID"
2. You will be redirected to the long URL that corresponds to the short URL with the given ID

## Tests
_**Example POST request using curl:**_
```
curl -v -X POST http://127.0.0.1:8080/shorten -H "Content-Type: application/json" -d '{"url": "http://example.com/verylonguselessURLthatdoesnotseemtoend/123"}'
```
Response:
```
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 8080 (#0)
> POST /shorten HTTP/1.1
> Host: 127.0.0.1:8080
> User-Agent: curl/7.55.1
> Accept: */*
> Content-Type: application/json
> Content-Length: 72
>
* upload completely sent off: 72 out of 72 bytes
< HTTP/1.1 201 Created
< Content-Type: application/json
< Date: Thu, 04 Mar 2021 03:17:30 GMT
< Content-Length: 47
<
{"short_url":"http://127.0.0.1:8080/2SMtYvSg"}
* Connection #0 to host 127.0.0.1 left intact
```


_**Example GET request using curl:**_
``` 
curl -v -X GET http://127.0.0.1:8080/2SMtYvSg
```
Response:
```
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 8080 (#0)
> GET /2SMtYvSg HTTP/1.1
> Host: 127.0.0.1:8080
> User-Agent: curl/7.55.1
> Accept: */*
>
< HTTP/1.1 302 Found
< Content-Type: text/html; charset=utf-8
< Location: http://example.com/verylonguselessURLthatdoesnotseemtoend/123
< Date: Thu, 04 Mar 2021 03:17:59 GMT
< Content-Length: 84
<
<a href="http://example.com/verylonguselessURLthatdoesnotseemtoend/123">Found</a>.

* Connection #0 to host 127.0.0.1 left intact
```
