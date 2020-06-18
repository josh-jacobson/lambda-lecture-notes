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

## Redux and React: connect
Then we **connect** a component to the Redux store, we're providing a very friendly interface for a component to be able to interact with the Redux store. 

We can still work with `useState` for managing state at the component level, but for bigger-picture concerns of our application we'll make the Redux store our single source of truth. With the two arguments we provide to **connect**, we set up both directions of communication:
* `mapStateToProps` indicates the state values to be provided from the store to our component, as props
* `mapDispatchToProps` sets up convenient standalone functions for the store, so that within the component we can simply call these functions rather than worrying about the additional complexity of dispatching actions to a reducer. 

In effect the interface becomes pretty similar to how we managed state before learning about reducers and all of these additional abstractions. Our component receives the most up-to-date values from the store as props, and to update the store we just call normal functions.

Now that you know what connect does, let's revel in it's (confusing at first) higher-order-function format:
```javascript
// before connecting: export default Title;
export default connect(mapStateToProps,mapDispatchToProps)(Title);
```

Calling `connect` returns another function, which we then invoke on our Title component in order to "enhance" the component with these new features described above. All of this functional programming stuff can get confusing, so just remember the key idea that we're **connect**ing commponents so that they can interact with the Redux store. After writing this boilerplate code, our components receive the values they need from the store as well as functions to update the store, all as props.

## Behind the 'magic': action creators and mapDispatchToProps object shorthand
In Redux we'll use a slightly different pattern than we used with the `useReducer` hook. Rather than dispatching actions directly, we'll follow a different pattern that allows Redux to do more of the work for us. The first step is to define  *action creators*, functions that return each action. Like this:

```javascript
// updateTitle action creator
export const updateTitle = newTitle => {
  return { type: "UPDATE_TITLE", payload: newTitle };
};
```
Then we can use those action creators in `mapDispatchToProps` like this:
```javascript
const mapDispatchToProps = dispatch => {
  return {
    updateTitle: newTitle => dispatch(updateTitle(newTitle)),
    toggleEditing: () => dispatch(toggleEditing()),
    // other actions here
  };
```
Within our component, we can just call `props.updateTitle` with our new title, and an action will be dispatched to the reducer. So we get all of the power of reducers and application-level state management, with the simplicity of just calling a regular old function. This mapping of *action creators* to functions with the same name is the pattern behind the magic here, and React Redux simplifies things one step further by allowing us to just pass in an object rather than a function for `mapDispatchToProps`:
```javascript
// This works just the same as the more verbose version above
const mapDispatchToProps = {updateTitle, toggleEditing}
```

Behind the scenes, React Redux calls `bindActionCreators({updateTitle, toggleEditing}, dispatch)` to convert the shorthand object into the actual dispatch mapping function we need for `connect`. We'll generally just use the shorthand, but feel free to write it out the long way at first and you may find that it makes the whole concept a bit more clear. 

React Redux takes this one step further
## Helpful Resources
* [Redux Glossary](https://redux.js.org/glossary)
* [connect, mapStateToProps, mapDispatchToProps (react-redux Docs)](https://react-redux.js.org/api/connect)
* [Codevolution React Redux tutorial](https://www.youtube.com/playlist?list=PLC3y8-rFHvwheJHvseC3I0HuYI2f46oAK)
* [A Cartoon Intro to Redux](https://code-cartoons.com/a-cartoon-intro-to-redux-3afb775501a6)
