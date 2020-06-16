# Async Redux

## A Real-World Example
Back to our coffee shop. Let's consider just the step where we actually make the coffee.

When we dispatch `'MAKE_COFFEE'`, we're actually looking to trigger a sequence of coffee-making actions. We could of course break everything down into individual steps, but all actions in Redux are **synchronous** by default. But do we really want to stand there and watch the beans grind? We can get things done more efficently with some multiasking. 

Enter `redux-thunk`, which allows our actions to dispatch actions of their own and introduce more advanced behavior like API calls and other side effects.

Rather than simply passing an action type and payload to the reducer, we can start multiple processes at once and set up some intelligent multitasking. Start the bean grinder, then steam some milk while the beans grind. Once the beans are ground, then we can start the espresso machine. Once the espresso is brewed and milk frothed, then we can put it all together and serve the drink. All of that work can be divided up in an efficient way, even split among multiple employees and several espresso machines to handle more than one order at once. 

Note that there's a specific order of operations, with some actions requiring others to be done before others can begin.  *Synchronous* actions take place in sequential order, each action waiting for the previous one to complete before starting. Meanwhile, our *asynchronous* actions like grinding beans and frothing milk can be occurring simultanouesly, in the background.  The key to the fast, responsive feel of single-page applications is this asynchronous behavior -- different action take place on their own timeline, sometimes simultaneously, and no one is stopping to watch the beans grind. 

This kind of thing is common with asynchronous actions like API calls in React applications -- start the process, go do something else, then come back to handle the response when it's complete. When the code gets confusing, remember this example to understand what asynchronous actions are all about. 

Here's how that `MAKE-COFFEE` step might look above, in a coffee subcomponent:
  * Dispatch `'GRIND_BEANS'`
  * Dispatch `'FROTH_MILK'`
  * When bean grinding is complete, dispatch `'BREW_ESPRESSO'`
  * when `'BREW_ESPRESSO'` and `'FROTH_MILK'` are complete, dispatch `'MAKE_MACCHIATO'`
  * when macchiato is complete, update application state

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
