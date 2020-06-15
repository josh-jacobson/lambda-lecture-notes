# Redux

## Review: Reducers
In the context of React and state management, a reducer is a pure function that takes the previous state and an action, and returns the next state:
```javascript
reducer = (previousState, action) => nextState
```

## 3 core concepts of Redux
1. Store - holds the state of your application
2. Action - describes the changes in the state of the application
3. Reducer - actually carries out the state transition depending on the action

## 3 principles of Redux
1. The state of your whole application is stored in an object tree (maintain our application state in a single object which is managed by Redux)
2. The only way to change the state is to emit an action, an object describing what happened. (i.e., you’re not allowed to directly update the state object)
3. To specify how the state tree is transformed by actions, you write pure reducers.


## Actions
* Are the only way your application can interact with the store
* Are plain Javascript objects
* Have a 'type’ property, a string constant indicating the type of action being performed 

## Hierarchy of State
Without a state management system like Redux, our only notion of state is at the level of each component and all interactions must be achieved with “prop drilling”, passing data and state management functions down the component tree. Redux is all about consolidating this and managing **application-level state**.

We also have the newer Context API to work with, and you'll hear about these three main "levels" of state:
* Application-level state
* Context-level state
* Component-level state
