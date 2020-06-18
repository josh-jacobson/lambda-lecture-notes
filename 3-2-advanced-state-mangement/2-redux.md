# Redux

## Review: Reducers
In the context of React and state management, a reducer is a pure function that takes the previous state and an action, and returns the next state:
```javascript
reducer = (previousState, action) => nextState
```

Here are the three main aspects of the reducer pattern:
* **Reducer**: takes an action and current state (both objects!) and returns the new state
* **Action**: object that includes a string specifying the type of action to be performed, and any data needed by the reducer to properly update state (e.g., the text inputted by a user in a form)
* **Dispatch function**: *dispatches* an action to the reducer

An "action" is simply an object with this format:
```javascript
const action = {
  type: 'UPDATE_TITLE' // action types are UPPER_CASE string constants by convention
  payload: 'New Title' // data needed to update state
}
```

## 3 core concepts of Redux
1. Store - holds the state of your application
2. Action - describes the changes in the state of the application
3. Reducer - actually carries out the state transition depending on the action

## 3 principles of Redux
1. The state of your whole application is stored in an object tree (maintain our application state in a single object which is managed by Redux)
2. The only way to change the state is to emit an action (i.e., you’re not allowed to directly update the state object)
3. To specify how the state tree is transformed by actions, you write pure reducers.

## Actions
* Are the only way your application can interact with the store
* Are plain Javascript objects
* Have a 'type’ property, a string constant indicating the type of action being performed 

## Managing shared state across multiple components
Without a state management system like Redux, our only notion of state is at the level of each component and all interactions must be achieved with “prop drilling”, passing data and state management functions down the component tree. Redux is all about consolidating this and managing **application-level state**.

We also have the newer Context API to work with, and you'll hear about these three main "levels" of state:
* Application-level state
* Context-level state
* Component-level state

## Helpful Resources
* [Redux Glossary](https://redux.js.org/glossary)
* [connect, mapStateToProps, mapDispatchToProps (Redux Docs)](https://react-redux.js.org/api/connect)
* [Codevolution React Redux tutorial](https://www.youtube.com/playlist?list=PLC3y8-rFHvwheJHvseC3I0HuYI2f46oAK)
* [A Cartoon Intro to Redux](https://code-cartoons.com/a-cartoon-intro-to-redux-3afb775501a6)
