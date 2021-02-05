# Class Components

## Objectives
* Explain class components, and use a class component to render some state data to the DOM
* Share data between components using state and props
* Respond to events triggered by user interaction and handle user input via forms in React
* Understand the foundations of React by seeing how things work "under the hood", before Hooks simplified the interface for developers
* (looking ahead to the next sprint) Start getting comfortable with "component-level" vs "application-level" state

## Are class components still relevant?

Function components were originally limited in their abilities, but React 16.8 introduced Hooks, allowing function components to "hook into" state and side effects without the need for class components.

Hooks streamline things a lot, and most developers prefer writing new components this way. But you'll also learn something new about the philosophy and principles behind React by learning the "old way" with class components.

And in the real world, you'll usually encounter applications with a mix of class and function components, so it'll help a lot in your career to fully understand both styles.

## Class components vs Function components:
  * Class components have just one state variable, an object with multiple keys. We use `this.setState` to update state
  * Function components may have one or more state variables, managed with `useState` and/or `useReducer`
  * What gets rendered to the DOM? When using class components, it's the JSX returned by the `render()` method. For function components, the component itself is simply a function and its return value is the JSX that gets rendered. 
  * In class components we use lifecycle methods to manage state and side effects. For function components we use Hooks.
  * Hooks cannot be used in class components! (and lifecycle methods are not used in function components)

## Anatomy of a Class Component

Here's a commented example showing all of the pieces of a typipical React class component:

```javascript
class Lambda extends React.Component {
  constructor() {
    super(); // calls the constructor from React.Component, which intializes this.props
    // initialize state here:
    this.state = {
      // For each state value that you'd manage with useState in a function component, 
      // create a key here on the class component's unified state object:
      firstName: "josh",
      lastName: ""
    }
  }
  
  // lifecycle methods: 
  // componentDidMount, componentDidUpdate, componentWillUnmount (all three together are equivalent to useEffect)
  componentDidMount() {
    // Use this.setState() to update state (never use equals assign outside of the constructor!)
    // setState performs a "shallow merge" on the state object, meaning that only the keys you include are updated. 
    // For example, here we can update lastName while leaving firstName as is:
    this.setState({lastName: "jacobson"}); 
  }
  
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

export default Lambda;
```

The base Component class includes built-in functionality for handling state and props, with specific methods that run at various points throughout the component's "lifecycle" (from mounting in your app, to updating, and eventually unmounting -- we'll study these in the next lecture).

The default `React.Component` constructor initializes `this.props` and other useful things -- feel free to look at the [React.Component constructor source code](https://github.com/facebook/react/blob/1d25aa5787d4e19704c049c3cfa985d3b5190e0d/packages/react/src/ReactBaseClasses.js#L22) if you're curious about what that `super()` call actually does.


## Bonus: ES6 classes and function prototypes in JavaScript

A good random fact to know for your coding interviews is that Javascript is built on "prototype-based inheritance", a simpler version of the traditional class-based inheritance found in other languages like Java and C++. Though we're now used to seeing `class` terminology used in newer ES6 syntax, Javascript does handle things a bit differently under the hood, and it's worth understanding the differences. 

ES6 has changed things for the better, allowing inheritance without having to write a lot of messy, potentially confusing code. You'll almost always end up just writing ES6 classes because they're nicer and easier to understand, but just remember that your ES6 code compiles down to vanilla Javascript and it's the same prototype-based inheritance model at play. Let's take a look at how object-oriented programming works in JavaScript with and without ES6 classes, and try to demystify thigs a bit.

These are effectively the same:

```javascript
// plain old Javascript -- defining a constructor function
function Person(name, favoriteGenre) {
  this.name = name;
  this.genre = favoriteGenre;
}

// Define methods on the prototype:
Person.prototype.listen = function() {
  console.log(this.genre);
}

josh = new Person("josh", "jazz");
josh.listen();
```

```javascript
// ES6
class Person {
  constructor(name, favoriteGenre) {
    this.name = name;
    this.genre = favoriteGenre;
  }
  
  // ES6 abstracts away the prototype complexity so we can just define a class method right here:
  listen = () => {
    console.log(this.genre);
  }
}
josh = new Person("josh", "jazz");
josh.listen();
```

ES6 provides a syntax for object-oriented programming that is more familiar to software developers from more traditional object-oriented languages (e.g., C++, Python, Ruby), but this syntax doesn't actually change the protoype-based inheritance model of JavaScript. 

In other languages, a class constructor creates an instance of the class, but a constructor in JavaScript is simply a function that returns an object. You've seen constructors like `String`, `Array` and `Object` that are built into JavaScript and we've also defined our own. The subtle differences between true class-based OOP and what we do in JavaScript won't make much difference for our purposes in React, but just know that Babel compiles your ES6 `class` down to a constructor function and definitions on its prototype.

In React, when we define a class component that `extends React.Component` we're basically just taking that pre-defined base component class and extending it with our own custom behavior.



## Helpful Resources
[How ES6 classes really work](https://medium.com/@robertgrosse/how-es6-classes-really-work-and-how-to-build-your-own-fd6085eb326a)

[Using arrow functions to avoid binding `this` in React](https://medium.com/@joespinelli_6190/using-arrow-functions-to-avoid-binding-this-in-react-5d7402eec64)

[React.Component documentation](https://reactjs.org/docs/react-component.html)

[State and Lifecycle](https://reactjs.org/docs/state-and-lifecycle.html)

  
