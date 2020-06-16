# The Reducer Pattern

## Data types and pointers in JavaScript
In Javascript there are several "primitive data types" (e.g., `Number`, `String`, `Boolean`), each of which stores a value of a fixed size in memory. For example, a Number type is always exactly 8 bytes of data, to store a 64-bit floating point value.

How big is an array or object though? These more advanced data structures can be of any size, and require a more complicated system of memory allocation and management. So an Object actually stores a "pointer" to another memory location, where the right amount of storage space can be dynamically allocated.

So `Object` in Javascript is known as a "reference type" rather than a "primitive type". For reference types we store a pointer to another memory location rather than storing a fixed amount of data directly. Since all non-primitive data structures (including Array and the mutable String object) inherit from this same Object prototype in JavaScript, we're actually always working with pointers. 

That may all be a bit abstract at first, so here's how it applies in practice:

```javascript
// Using = to copy objects just duplicates the pointer, not the object itself
const obj = {name: "josh", color: "blue"};
const obj_two = obj;
obj_two.color = "red";

console.log(obj, obj_two); // both have color: red
// This leads to unintended side effects! 

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
Say you're starting a local business, like a coffee shop. Throughout the course of a day there are many different actions to be done -- grinding beans, making espresso, accepting payments, and so on. Within a single transaction with a customer, there are several state changes that take place and we'd like them to take place in a specific order. Once the customer pays we'll "dispatch" an action to update the state of their order and kick off the process of making their coffee. Here's an example, in the language of reducers:

* Initial state. `{order: '', cost: null, status: 'ordering'}`
* Customer orders. Dispatch action `'PLACE_ORDER'` with payload `'oat milk macchiato'`
* State updated. New state: `{order: 'oat milk macchiato', cost: 3.50, status: 'ordered'}`
* Dispatch action `'ACCEPT_PAYMENT'`
* State updated. New state: `{order: 'oat milk macchiato', cost: 3.50, status: 'paid'}`
* Dispatch action `'PREPARE_COFFEE'`
* State updated. New state: `{order: 'oat milk macchiato', cost: 3.50, status: 'preparing'}`
* Within this we might have a subcomponent specifically for making the coffee, with its own state representing the various stages of preparing espresso and milk. These would be the lower-level actions to be dispatched:
  * Dispatch `'GRIND_BEANS'`
  * Dispatch `'FROTH_MILK'`
  * When bean grinding is complete, dispatch `'BREW_ESPRESSO'`
  * when `'BREW_ESPRESSO'` and `'FROTH_MILK'` are complete, dispatch `'MAKE_MACCHIATO'`
* State updated. New state: `{order: 'oat milk macchiato', cost: 3.50, status: 'complete'}`
* Dispatch action `'SERVE_COFFEE'`

Even in this simplistic coffee example, you can imagine how things get complicated quickly. For a small menu we could easily have 20+ different actions. Rather than hiring a new employee for each action, we hire a skilled barista who can juggle all of these different tasks and keep things organized in the process.

Likewise, when managing state in a React application, we're not going to want to write a separate state management function for every possible state transition. Instead, a **reducer** can play the role of barista and handle all of these actions in an organized, predictable way. 

Note also that some of the actions above are *synchronous* (taking place in sequential order, each action waiting for the previous one to complete before starting) while some, like `'GRIND_BEANS'` and `'FROTH_MILK'`, are *asynchronous*, meaning that they can take place simultaneously, with some multitasking optimization rather than just watching the beans grind. This kind of thing is common with asynchronous actions like API calls in React applications -- start the process, go do something else, then come back to handle the response when it's complete. We'll be learning bout that in depth next week, but just consider this real-world example for now and refer back to this idea for grounding when the code gets confusing.

## Reducers in React
A reducer is a pure function that takes the previous state and an action, and returns the next state. It "reduces" those two arguments to one output:

```javascript
reducer = (previousState, action) => nextState
```

So in React, a reducer can effectively do the work of several different state management functions, all wrapped into one. Here are the three main aspects of the pattern:
* **Reducer function**: takes an action and current state, returns the new state
* **Action**: object that includes a string specifying the type of action to be performed, and any data needed by the reducer to properly update state (e.g., the text inputted by a user in a form)
* **Dispatch function**: *dispatches* an action to the reducer

And an "action" is simply an object with this format:
```javascript
const action = {
  type: 'TAKE_ORDER' // action types are UPPER_CASE string constants by convention
  payload: 'oat milk macchiato' // data needed to update state
}
```

## useReducer Hook
We're not diving into Redux just yet, but we can start getting comfortable with the Reducer pattern and all of its conventions by working with the `useReducer` hook, an alternative to `useState`. Here's how it works:

```javascript
function reducer(state, action) {
  switch (action.type) {
    case 'TAKE_ORDER':
      return {...state, order: action.payload, status: 'ordered'}; 
      // also define order cost here
    case 'ACCEPT_PAYMENT':
      return {...state, status: paid};
    // other actions
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

Redux builds on this pattern to provide a "predictable state container", and over the next two weeks we'll be learning about various ways of managing application-level and context-level state with Redux and Context API. Things can get confusing with the amount of abstraction involved, but as long as you're really solid on these fundamentals you'll be good to go.

## Helpful Resources:
* [JavaScript data types - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
* [Primitive vs Reference Values](https://www.javascripttutorial.net/javascript-primitive-vs-reference-values/)
* [useReducer vs useState](https://www.robinwieruch.de/react-usereducer-vs-usestate)
* [useReducer Hook](https://reactjs.org/docs/hooks-reference.html#usereducer)
* [Reducers, from the Redux Docs](https://redux.js.org/basics/reducers)
