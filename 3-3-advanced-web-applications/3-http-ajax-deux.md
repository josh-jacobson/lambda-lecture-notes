# HTTP / AJAX II

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
| put               | Update           | Update a resource                   | 200 (OK) or 201 (created)    |
| delete            | Delete           | Delete a resource                   | 200 (OK) or 204 (no content) |

Most modern API's conform to the "representational state transfer" (REST) architecture, with a standardized format for how the "endpoints" (the addresses you send your API calls to) are laid out and how they behave. For example, a typical RESTful resource endpoint might look like this:

* GET /users        (get all users)
* GET /users/123    (get user with id '123')
* POST /users       (create a new user, with data in payload)
* PUT /users/123    (update user 123 with data in payload)
* DELETE /users/123 (delete user 123)

It's also common for API endpoints to be "namespaced" with something like "v1/" to indicate the api version, and to have additional nesting based on the structure of your app.

## PUT and DELETE
Today's lecture is all about these two HTTP verbs, which we haven't used as much as GET or POST so far. 

## Helpful Resources
* [RESTful Web Services tutorial](https://www.tutorialspoint.com/restful/restful_introduction.htm)
* [A Brief Introduction to REST](https://www.infoq.com/articles/rest-introduction/)
