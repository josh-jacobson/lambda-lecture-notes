# Async Redux

## Redux Middleware
In the context of Redux, middleware is a way to extend the standard functionality with additional behavior, Middleware provides a third-party extension point after an action is disaptched, before it reaches the reducer:

Dispatching an action
->
middleware
->
Action reaching the reducer

Redux middleware is often used for logging, crash reporting, talking to an asynchronous API, routing, and more. `redux-logger` and `redux-thunk` are common examples of middleware used with Redux.

## How to use middleware in Redux
Redux library provides a function called applyMiddleware. This gets applied like this:

```javascript
const logger = reduxLogger.createLogger();
const store = createStore(rootReducer, applyMiddleware(logger));
```

## Asynchronous requests and redux-thunk
In Redux, our reducers are *synchronous* by default. If we need to perform asynchronous operations, they need to happen before the actions reach the reducers. So this is why we use middleware to handle asynchronous requests. 

"Thunk" is a name for a function that’s returned by another function. In Redux, actions are normally just objects, but Redux-thunk allows us to return functions instead of objects from our action creators, enabling more dynamic behavior. Then those functions can handle side effects like api calls, and also return regular actions to be handled by the reducer.

Here's a typical setup:
* Use redux-thunk as a middleware, and define async action creators
* Within those async actions, use axios to make requests to an api endpoint

## Helpful Resources
* [What is a thunk?](https://daveceddia.com/what-is-a-thunk/)
