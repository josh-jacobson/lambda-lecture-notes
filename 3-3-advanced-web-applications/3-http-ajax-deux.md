# HTTP / AJAX II

## Review: HTTP, CRUD and RESTful services
Most modern API's conform to the "representational state transfer" (REST) architecture. Here's a cheat sheet for how to interact with server-side web services from a front-end client like the React apps we're building:

| HTTP Verb (axios) | CRUD naming      | Description                         | Happy Path                   |
|-------------------|------------------|-------------------------------------|------------------------------|
| get               | Read             | Read a representation of a resource | 200 (OK)                     |
| post              | Create           | Create new resources                | 201 (created)                |
| put               | Update           | Update a resource                   | 200 (OK) or 201 (created)    |
| delete            | Delete           | Delete a resource                   | 200 (OK) or 204 (no content) |


## Helpful Resources
