# Client-Side Authentication

## Objectives
At the end of this module, you should be able to:
* handle authentication with tokens in a React app
* implement protected routes using an authentication token and Redirect

## JSON Web Tokens (jwt)

## Review: Local Storage
For your Auth Friends project, you'll be using an auth token to make requests to protected API endpoints. After initial authentiction, saving the returned auth token locally is a common practice for allowing the user to remain "logged in." We'll use Local Storage for this, since it provides a very straightforward way of saving key/value pairs locally. Here's a quick review:
s
```javascript
localStorage.setItem('key', 'value');
localStorage.getItem('key'); // returns 'value
```

You'll sometimes need `localStorage.removeItem` and `localStorage.clear()` for cleanup, but that's basically the entire API! Nice and simple. Note that there are other, more secure methods of saving JWT auth tokens locally and `localStorage` is rarely a good choice for this in practice. But the functionality is similar in principle, so this approach provides a great introduction to the topic for learning purposes.

## HTTP and CRUD for RESTful services
Since you'll also be working directly with an API for the Auth Friends project, here's a quick review / cheat sheet for how to interact with web services. Most modern API's conform to this common "representational state transfer" (REST) architecture.

| HTTP Verb (axios) | CRUD naming      | Description                         | Happy Path                   |
|-------------------|------------------|-------------------------------------|------------------------------|
| get               | Read             | Read a representation of a resource | 200 (OK)                     |
| post              | Create           | Create new resources                | 201 (created)                |
| put               | Update           | Update a resource                   | 200 (OK) or 201 (created)    |
| delete            | Delete           | Delete a resource                   | 200 (OK) or 204 (no content) |

Log any errors out to the console from your axios requests while building out a client, and keep an eye out for these common error codes (sad path!) that may show up. Understanding what they mean will make debugging a lot easier:

400 Bad Request
You sent an invalid JSON document (e.g. a "}" is missing), or the syntax/content is incorrect.

401 Unauthorized
The access credentials (via the Authorization header) were missing or are invalid.

403 Forbidden
The credentials you provided are valid, but you are not authorized to access the resource you requested.

404 Not found
The request itself is valid, but the resource you try to access does not exist, or is outside your scope.


## Videos
[Protected Routes in React using React Router](https://www.youtube.com/watch?v=Y0-qdp-XBJg)
[React Client Side Authentication](https://www.youtube.com/watch?v=oRL-pttfNSc)

## Articles
[Introduction to JSON Web Tokens](https://jwt.io/introduction/)
[Protected Routes - React tutorial](https://medium.com/javascript-in-plain-english/how-to-set-up-protected-routes-in-your-react-application-a3254deda380)
[Building Basic React Authentication](https://medium.com/better-programming/building-basic-react-authentication-e20a574d5e71)
[Introduction to Local Storage](https://sebhastian.com/local-storage-introduction)
[HTTP Verbs and Error Codes](https://developers.evrythng.com/docs/http-verbs-and-error-codes)
