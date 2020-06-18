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

## Higher Order Components
A higher-order component (HOC) is a function that takes a component and returns a new component:
```javascript
const EnhancedComponent = higherOrderComponent(WrappedComponent);
```

In the context of Redux, we'll be using this pattern with the `connect` function in order to "enhance" the components of our application with the ability to seamlessly update and read from the Redux store.

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

## Updating and reading from the Redux store
We can still work with `useState` for managing state at the component level, but for bigger-picture concerns of our application we'll make the Redux store our single source of truth. 

So how does it all work? We use a function called `connect`, which takes two arguments corresponding to the two direction of communication (read and write). Here's what they mean, on a high level:
* `mapStateToProps`: which parts of application-level state are relevant to you (the component)? Let me (Redux) know and I'll keep you up to date, sending over those values directly as props whenever the store is updated.
* `mapDispatchToProps`: in what specific ways would you (the component) like to be able to update the store? List each action here and I'll provide a corresponding function for each one, passed to you as props. When you're looking to update application-level state, just call one of those functions and you're done. I'll handle all the reducer-y stuff for you.

When we **connect** a component to the Redux store, we're providing a helpful interface to be able to update our component with the latest application-level state, and also trigger updates to the application-level state from our component.

The way we actually set things up is a bit complex, but the goals behind this pattern are intuitive -- just remember that the whole idea is for components to be able to communicate with the store, to both read and write.

In effect the interface becomes somewhat similar to how we managed state before learning about reducers and all of these additional abstractions. Our component receives the most up-to-date values from the store as props, and to update the store we just call functions that are also passed in as props.

## Putting it all together: `connect`

Now that you know what connect does, let's revel in its (admittedly confusing) HOC format:
```javascript
// without Redux: export default Title;
// with Redux, connecting Title component to the store:
export default connect(mapStateToProps,mapDispatchToProps)(Title);
```

`connect` is itself a  a higher order function that *returns* a higher order component, which we then immediately invoke on our Title component in order to "enhance" it. That's a lot to take in, and if all this functional programming stuff feels like Inception to you, you're not alone. But the "enhancement" we're going for with all this is simply the ability to interact with the store. 

Just remember the key idea here: **we `connect` commponents so that they can communicate with the Redux store.**

Once we've written this boilerplate code, most of the complexity is abstracted away and each component is enhanced with this convenient interface to interact with the store:
* State relevant to the component gets passed in as props (updated with every application state change)
* Functions to update application state also get passed to the component as props. (Each of these functions dispatches a corresponding action to a reducer in order to update the Redux store)

## Behind the 'magic': action creators and mapDispatchToProps object shorthand
In Redux we'll use a slightly different pattern than we used with the `useReducer` hook. Rather than dispatching actions directly from our components, we define  *action creators*. An action creator is just a function that returns an action object: 

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

## Helpful Resources
* [Redux Glossary](https://redux.js.org/glossary)
* [React Redux docs: connect, mapStateToProps, mapDispatchToProps](https://react-redux.js.org/api/connect)
* [Codevolution React Redux tutorial](https://www.youtube.com/playlist?list=PLC3y8-rFHvwheJHvseC3I0HuYI2f46oAK)
* [A Cartoon Intro to Redux](https://code-cartoons.com/a-cartoon-intro-to-redux-3afb775501a6)
