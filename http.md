# What is the web and how does HTTP fit in?

# HTTP: Hypertext Transfer protocol

## What is Hypertext and what is a protocol?
A protocol is a system of rules that allows the communication of information between two entities, like computers.
Hypertext is text that appears on a computer screen that contains text to other links.


## REQUESTS AND RESPONSES
---
### Anatomy of a URL
### HTTP Methods
* GET - only neets method and URL.
* POST - creates a new resource. needs authorization header
* PUT - update an existing resource
* PATCH - modify an existing resource
* DELETE - deletes a specified resource. 
* HEAD - returns just the head of the response
* OPTIONS - returns a list of the options for the communication resource
* TRACE - creates a loopback for the request message

### HTTP Status Codes

1XX - Information

2XX - Success
* 200 OK
* 201 created
* 204 no content

3XX - Redirection
* 301 moved permanently
* 302/303 found. temporary redirected 
* 307
* 308

4XX - Client Error
* 400 Bad Request
* 401 Unauthorized
* 403 Forbidden
* 404 Not Found
* 405 Method not Allowed

5XX - Server Error
* 500 Internal Server error
* 502 Bad Gatewat
* 503 Service unavailable


## HTTP Headers
---
### What are HTTP Headers?
An HTTP header is a human readable name value pair separated by a colon, added to the HTTP request or response, which can be used to pass standard or custom information back and forth between the client and the server. A request can hold as many headers as are needed, each separated by a line break.
### Anatomy of a Request Header
### Anatomy of a Response Header
### Cookies
### Sessions