# Class Components

## Review: JavaScript function prototypes and ES6 classes

Javascript is a prototype-based language, with a style of object-oriented programming that makes use of cloning rather than classes. JavaScript objects inherit properties and methods from a prototype. It's a popular convention to capitalize constructors

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

ES6 provides a syntax for object-oriented programming that is more familiar to coders from more traditional object-oriented languages (e.g., C++, Python, Ruby), but this syntax doesn't actually change the protoype-based inheritance model of JavaScript. 

In other languages, a class constructor creates an instance of the class, but a constructor in JavaScript is simply a function that returns an object. You've seen constructors like `String`, `Array` and `Object` that are built into JavaScript and we've also defined our own. The differences between true class-based OOP and what we do in JavaScript won't make much difference for our puroses in React, but just know that Babel compiles down to a function prototype definition when you define an ES6 `class`. 

In react, when we define a class component that `extends React.Component` we're basically just cloning that base component class and extending it with our own custom behavior.

## Class Components

React development originally focused on class components, written like this:

```javascript
class Lambda extends React.Component {
  constructor() {
    super(); // calls the constructor from React.Component, which passes props
    // initialize state here
  }
  
  // lifecycle methods: componentWillMount, componentDidMount, componentWillReceiveProps, shouldComponentUpdate, componentWillUpdate, componentDidUpdate, and componentWillUnmount
  
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

export default Lambda;
```

The base Component class includes built-in functionality for handling state and props, with specific lifecycle methods that run at different points throughout the component's "lifecyele" (from mounting in your app, to updating state, and eventually unmounting -- we'll study these in the next lecture).

The default `React.Component` constructor initializes `this.props` and other useful things -- feel free to look at the [React.Component constructor source code] (https://github.com/facebook/react/blob/1d25aa5787d4e19704c049c3cfa985d3b5190e0d/packages/react/src/ReactBaseClasses.js#L22) if you're curious about what that `super()` call actually does.

Function components were originally limited in their abilities, but React 16.8 introduced Hooks, allowing function components to "hook into" state and side effects without the need for class components.

Hooks streamline things a lot, and most developers prefer writing new components this way. However, you'll learn about the philosophy and principles behind React by learning the "old way" with class components.

And in the real world, you'll usually encounter applications with a mix of class and function components, so it'll help a lot in your career to fully understand both styles.

## Class components vs Function components:
  * In class components we use lifecycle methods to manage state and side effects. For function components we use Hooks.
  * Hooks cannot be used in class components! (and lifecycle methods are not used in function components)
  * Class components have just one state variable, an object with multiple keys
  * Function components have the option to store state in one or multiple variables, managed with `useState` and/or `useReducer`


## Helpful Resources
[How ES6 classes really work](https://medium.com/@robertgrosse/how-es6-classes-really-work-and-how-to-build-your-own-fd6085eb326a)

[Using arrow functions to avoid binding `this` in React](https://medium.com/@joespinelli_6190/using-arrow-functions-to-avoid-binding-this-in-react-5d7402eec64)

[React.Component documentation](https://reactjs.org/docs/react-component.html)

[State and Lifecycle](https://reactjs.org/docs/state-and-lifecycle.html)

  
