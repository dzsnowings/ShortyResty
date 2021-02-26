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
curl -v -H "Content-Type: application/json" -X POST -d "{\"url\": \"http://example.com/verylonguselessURLthatdoesnotseemtoend/123\"}" http://127.0.0.1:8080/shorten
```
Response:
```
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 8080 (#0)
> POST /shorten HTTP/1.1
> Host: 127.0.0.1:8080
> User-Agent: curl/7.55.1
> Accept: */*
> Content-Type: application/json
> Content-Length: 32
>
* upload completely sent off: 32 out of 32 bytes
< HTTP/1.1 201 Created
< Content-Type: application/json
< Date: Fri, 26 Feb 2021 06:51:54 GMT
< Content-Length: 47
<
{"short_url":"http://127.0.0.1:8080/2SMtYvSg"}
* Connection #0 to host 127.0.0.1 left intact
```


_**Example GET request using curl:**_
``` 
curl -v -H "Content-Type: application/json" -X GET -d "{\"short_url\": \"http://127.0.0.1:8080/rfBd56ti\"}" http://127.0.0.1:8080/$ID
```
Response:
```
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 8080 (#0)
> GET /$ID HTTP/1.1
> Host: 127.0.0.1:8080
> User-Agent: curl/7.55.1
> Accept: */*
> Content-Type: application/json
> Content-Length: 47
>
* upload completely sent off: 47 out of 47 bytes
< HTTP/1.1 302 Found
< Content-Type: text/html; charset=utf-8
< Location: http://www.google.com
< Date: Fri, 26 Feb 2021 06:52:30 GMT
< Content-Length: 44
<
<a href="http://www.google.com">Found</a>.

* Connection #0 to host 127.0.0.1 left intact
```
