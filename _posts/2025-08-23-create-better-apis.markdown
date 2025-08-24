---
layout: post
title:  "Create better APIs"
date:   2025-08-23 20:07:00 -0300
categories: rest apis
---

# Create better APIs:

**guess this will post will never be completed, if I discover something new, will come back here to update** 

#### Representational State Transfer (REST):
1. Resources – Everything you work with is a resource (users, comments, orders), each with a unique URL:
1. HTTP Verbs – Standard HTTP methods define what you do with resources:
   1. User and Comments example:
      1. GET -> /users/ -> List everything
      1. GET -> /users/123 -> show user with id 123 
      1. POST -> /users/ -> create a user
      1. DELETE -> /users/123 -> delete user with id 123 
      1. PUT -> /users/123 -> updates all the fields from user 123
      1. PATCH -> /users/123 -> updates specific fields from user 123
      1. GET -> /users/123/comment/ -> List all comments from user 123.
      1. GET -> /users/123/comment/123 -> show user 123 comment with id 123.
      1. POST -> /users/123/comment -> create a post for the user 123.
      1. GET --> /comment/123 -> show comment with id 123.
1. Clear, semantic URLs – URLs should clearly express the resource hierarchy or relationships

#### Principle of least surprise
Software should behave in a way that users or developers intuitively expect, minimizing surprises.

#### Stateless
Every request from the client to the server must contain all the information needed to understand and process the request. The server does not store any client session or context between requests.

#### Return proper status
1. Success (200)
   1. 200 -> OK -> Request succeeded -> General success for GET, PUT, DELETE
   1. 201 -> Created -> Resource successfully created	-> After POST creates a new resource
   1. 204 -> No Content ->	Request succeeded but no content to return -> After DELETE or PUT when no body is needed

1. Client error (4xx)
   1. 400 -> Bad Request -> Request invalid -> Missing fields, invalid JSON, or validation errors
   1. 401 -> Unauthorized -> Authentication required or failed -> No token, invalid credentials
   1. 403 -> Forbidden -> Authenticated but not allowed -> User has no permission for this resource
   1. 404 -> Not Found -> Resource not found -> Requested ID doesn’t exist
   1. 405 -> Method Not Allowed -> HTTP method not supported -> Using POST on a GET-only endpoint
   1. 409 -> Conflict -> Resource conflict -> Trying to create a resource that already exists
   1. 422 -> Unprocessable Entity -> Valid request but semantic error -> Validation failed on data

1. Server Errors (5xx)
   1. 500 -> Internal Server Error -> Unexpected server error -> Exceptions, database issues
   1. 501 -> Not Implemented -> Feature not supported -> API doesn’t support this action
   1. 502 -> Bad Gateway -> Upstream service failed -> API depends on another service
   1. 503 -> Service Unavailable -> Temporary downtime -> Maintenance or overload
   1. 504 -> Gateway Timeout -> Upstream service timed out -> Response took too long

#### Validate Inputs
1. Email should have an @
1. Telephone should not have letters.

Rule of thumb: Return all the errors. 

#### Pagination
Pagination is splitting a large dataset into smaller chunks, so you don’t send thousands of records in a single response.

1. Offset: number of items to skip before starting to return results from a dataset. It’s usually paired with a limit, which tells the server how many items to return.
Eg: GET /users?limit=10&offset=20 will skip the first 20 records and will only show 10 starting from them.


