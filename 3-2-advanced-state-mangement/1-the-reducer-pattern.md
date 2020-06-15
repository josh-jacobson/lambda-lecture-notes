# The Reducer Pattern

## Key Questions
Think about these main ideas (answered in the explanation below):
* Why is state immutable in React?
* Why do we create a new state object with the spread operator, rather than just modifying state directly?
* What is a reducer?
* Describe how dispatch functions, action objects, and reducer functions work together, and how we can use this pattern in React components with the `useReducer` hook.

## Data types and pointers in JavaScript
In Javascript, there are six "primitive data types" (`Number, String, BigInt, Symbol, Boolean, undefined`), each of which stores a value of a fixed size in memory. For example, a Number type is always exactly 8 bytes of data, to store a 64-bit floating point value.

How big is an array or object though? These more advanced data structures can be of any size, and require a more complicated system of memory allocation and management. So an Object actually stores a "pointer" to another memory location, where the right amount of storage space can be dynamically allocated.

This is why `Object` in Javascript is known as a "reference type" rather than a "primitive type". For reference types we store a pointer to another memory location rather than storing a fixed amount of data directly. Since all non-primitive data structures (including Array and the mutable String object) inherit from this same Object prototype in JavaScript, we're actually always working with pointers. 

That may all be a bit abstract at first, so here's how it applies in practice:

```javascript
// Copying objects this way just duplicates the pointer, not the object itself
// This leads to unintended side effects! 
const obj = {name: "josh", color: "blue"};
const obj_two = obj;
obj_two.color = "red";
console.log(obj, obj_two); // both have color: red

// That's why we create a new object every time, like this:
const josh = {name: "josh", color: "blue"};
const josh_two = {...josh, color: "red"};
console.log(josh, josh_two); // different colors
```
Because of the way we copied with =, obj and obj_two are pointers to the same object!! Equals assign does not create a new object. Be very careful with this and be aware of what’s going on.


## Immutability 
So we've seen that it's possible to create some unexpected side effects when working with these data structures in JavaScript if we aren't careful! In order to keep state changes and their effects throughtout the application **predictable**, we follow the convention of **immutable state** by creating an entirely new object with every state change. Note how the spread operator `...` helps streamline the syntax for this.

We've been following this convention all aong, but it becomes especially important once we start managing application state with Redux and Context API. 

## What is a Reducer?
In the context of React and state management, a reducer is a pure function that takes the previous state and an action, and returns the next state:
```javascript
reducer = (previousState, action) => nextState
```

And an "action" is simply an object with this format:
```javascript
const action = {
  type: 'INCREMENT_COUNTER' // action types are UPPER_CASE string constants by convention
  payload: {} // data needed to update state
}
```

## useReducer Hook
We're not diving into Redux just yet, but we can start getting comfortable with the Reducer pattern and all of its conventions by working with the `useReducer` hook, an alternative to `useState`. Here's how it works, based on a basic counter example from the React docs:

```javascript
function reducer(state, action) {
  switch (action.type) {
    case 'INCREMENT_COUNTER':
      return {count: state.count + 1};
    case 'DECREMENT_COUNTER':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'INCREMENT_COUNTER'})}>+</button>
      <button onClick={() => dispatch({type: 'DECREMENT_COUNTER'})}>-</button>
    </>
  );
}
```

So a reducer effectively does the work of several different state management functions, all wrapped into one function. Here are the three main aspects of the pattern:
* Reducer function: takes an action and current state, returns the new state
* Dispatch function: *dispatches* an action to the reducer
* Action: object that includes a string specifying the type of action to be performed, and any data needed by the reducer to properly update state (e.g., the text inputted by a user in a form)

Redux builds on this pattern to provide a "predictable state container", and over the next two weeks we'll be learning about various ways of managing application-level and context-level state with Redux and Context API. Things can get confusing with the amount of abstraction involved, but as long as you're really solid on these fundamentals you'll be good to go.

## Helpful Resources:
* [JavaScript data types - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
* [Primitive vs Reference Values](https://www.javascripttutorial.net/javascript-primitive-vs-reference-values/)
* [useReducer vs useState](https://www.robinwieruch.de/react-usereducer-vs-usestate)
* [useReducer Hook](https://reactjs.org/docs/hooks-reference.html#usereducer)
* [Reducers, from the Redux Docs](https://redux.js.org/basics/reducers)
