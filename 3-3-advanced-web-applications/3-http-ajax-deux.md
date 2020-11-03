# HTTP / AJAX II: PUT / DELETE

## Objectives
After today's guided project, you should be able to:
* make PUT requests to an external API using axios
* make DELETE requests to an external API using axios

## Review: HTTP, CRUD and RESTful services
Here's a cheat sheet for how to interact with server-side web services from a front-end client like the React apps we're building:

| HTTP Verb (axios) | CRUD naming      | Description                         | Happy Path                   |
|-------------------|------------------|-------------------------------------|------------------------------|
| get               | Read             | Read a representation of a resource | 200 (OK)                     |
| post              | Create           | Create new resources                | 201 (created)                |
| **put**               | Update           | Update a resource                   | 200 (OK) or 201 (created)    |
| **delete**            | Delete           | Delete a resource                   | 200 (OK) or 204 (no content) |

Most modern API's conform to the "representational state transfer" (REST) architecture, with a standardized format for how the "endpoints" (the addresses you send your API calls to) are laid out and how they behave. For example, a typical RESTful resource endpoint might look like this:

* GET /users        (get all users)
* GET /users/123    (get user with id '123')
* POST /users       (create a new user, with data in payload)
* PUT /users/123    (update user 123 with data in payload)
* DELETE /users/123 (delete user 123)

HTTP is a *protocol* that defines how servers and clients communicate over a network, essentially the foundation of the Internet as we know it. REST is an *architecture pattern* to standardize the way we build HTTP-based web services and clients. 

Side note for the routes shown above: it's very common for API endpoints to be "namespaced" with something like "v1/" to indicate the api version. Depending on the structure of your app, you might have endpoints with additional nesting, with a URL structure more like "api/v1/users".

## PUT vs POST
The difference between these two types of requests is fairly straightforward: POST to create a new resource, PUT to update an existing one. If you're ever unsure which to use, here's a good rule of thumb. 

**Does the resource I'd like to write to the database already exist?**
* If **yes**, we're **updating** that resource so we should use PUT.
* If **no**, we're **creating** a new resource and should use POST.

For both of these requests, we going the resource id along with data we'd like the API to write to the database. In practice, HTTP (the *HyperText Transfer Protocol*) doesn't strictly enforce any of this so it's up to you as the developer to think in terms of resources and follow the standard patterns of the REST architecture. Whether you're a front-end, back-end, or full-stack developer, knowing these patterns and best practices is extermely important for being able to write good code.

## DELETE
With a delete request, we simply pass the id of the resource to be deleted. It ends up looking quite similar to a GET request for a single resource, hitting the same URL and just using a different verb.

* GET /users/123    (get user with id '123')
* DELETE /users/123 (delete user 123)

## Helpful Resources
* [RESTful Web Services tutorial](https://www.tutorialspoint.com/restful/restful_introduction.htm)
* [A Brief Introduction to REST](https://www.infoq.com/articles/rest-introduction/)
* [AJAX Intro](https://www.w3schools.com/xml/ajax_intro.asp)
