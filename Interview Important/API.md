


### 1. What do you understand by RESTful Web Services?

RESTful web services are services that follow REST architecture. REST stands for Representational State Transfer and uses HTTP protocol (web protocol) for implementation. These services are lightweight, provide maintainability, scalability, support communication among multiple applications that are developed using different programming languages. They provide means of accessing resources present at server required for the client via the web browser by means of request headers, request body, response body, status codes, etc.

### 2. What are HTTP Status codes?

These are the standard codes that refer to the predefined status of the task at the server. Following are the status codes formats available:

-   1xx - represents informational responses
-   2xx - represents successful responses
-   3xx - represents redirects
-   4xx - represents client errors
-   5xx - represents server errors

Most commonly used status codes are:

-   200 - success/OK
-   201 - CREATED - used in POST or PUT methods.
-   304 - NOT MODIFIED - used in conditional GET requests to reduce the bandwidth use of the network. Here, the body of the response sent should be empty.
-   400 - BAD REQUEST - This can be due to validation errors or missing input data.
-   401- UNAUTHORIZED - This is returned when there is no valid authentication credentials sent along with the request.
-   403 - FORBIDDEN - sent when the user does not have access (or is forbidden) to the resource.
-   404 - NOT FOUND - Resource method is not available.
-   500 - INTERNAL SERVER ERROR - server threw some exceptions while running the method.
-   502 - BAD GATEWAY - Server was not able to get the response from another upstream server.



### Types of REST API method :

1. GET
2. POST
3. PUT -> For UPDATE 
	Generally, when a `PUT` request _creates_ a resource the server will respond with  `201` (`Created`), and if the request _modifies_ existing resource the server will return  `200` (`OK`) or `204` (`No Content`).
4. PATCH ->
A `PATCH` request is one of the lesser-known HTTP methods, but I'm including it this high in the list since it is similar to POST and PUT. The difference with `PATCH` is that you **only apply partial modifications to the resource**.
The difference between PATCH and PUT, is that a [PATCH request is non-idempotent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH) (like a POST request).
To expand on partial modification, say you're API has a `/users/{{userid}}` endpoint, and a user has a _username_. With a PATCH request, **you may only need to send the updated username** in the request body - as opposed to POST and PUT which require the full user entity.

5. DELETE - for deleting a resource
6. HEAD - 
The `HEAD` method is almost identical to `GET`, **except without the response body**. In other words, if `GET /users` returns a list of users, then `HEAD /users` will make the same request but won't get back the list of users.
HEAD requests are **useful for checking what a GET request will return** before actually making a GET request -- like before downloading a large file or response body.
_It's worth pointing out that not every endpoint that supports GET will support HEAD - it completely depends on the API you're testing._

7. OPTIONS
OPTIONS request should **return data describing what _other_ methods and operations the server supports** at the given URL.
OPTIONS requests are more loosely defined and used than the others, making them a good candidate to **test for fatal API errors**. If an API isn't expecting an OPTIONS request, it's good to put a test case in place that verifies failing behavior.

![[API_METHODS.png]]