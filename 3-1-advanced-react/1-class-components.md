# Class Components

## Javascript function prototypes and ES6 classes review

Javascript is a prototype-based language, with a style of object-oriented programming that makes use of cloning rather than classes. Javascript objects inherit properties and methods from a prototype.

These are effectively the same:

```javascript
// plain old Javascript -- defining a constructor function
function Person(name, favoriteGenre) {
  this.name = name;
  this.genre = favoriteGenre;
}
josh = new Person("josh", "jazz");
```

```javascript
// ES6
class Person {
  constructor(name, genre) {
    this.name = name;
    this.genre=genre;
  }
}
josh = new Person("josh", "jazz");
```

ES6 provides a syntax for object-oriented programming that is more familiar to coders from more traditional object-oriented languages (e.g., C++, Python, Ruby) but do not actually change the protoype-based inheritance model of Javascript. In other languages, a class constructor creates an instance of the class. A constructor in JavaScript is simply a function that returns an object. 

## Class Components

React development originally focused on class components, written like this:

```javascript
class Lambda extends React.Component {
  constructor() {
    super();
    // initialize state here
  }
  
  // lifecycle methods: componentWillMount, componentDidMount, componentWillReceiveProps, shouldComponentUpdate, componentWillUpdate, componentDidUpdate, and componentWillUnmount
  
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

export default Lambda;
```

The base Component class includes built-in functionality for managing state and other React features. We'll learn about the lifecycle methods of class components in the following lecture.

Function components were originally limited in their abilities, but React 16.8 introduced Hooks, allowing function components to "hook into" state without the need for class components.

Hooks streamline things a lot, and most developers prefer writing new components this way. However, you'll learn about the philosophy and principles behind React by learning the "old way" with class components.

And in the real world, you'll usually encounter applications with a mix of class and function components, so it'll help a lot in your career to understand both approaches.

## Class components vs Function components:
  * In class components we use lifecycle methods to manage state and side effects. For function components we use Hooks.
  * Hooks cannot be used in class components! (and lifecycle methods are not used in function components)
  * Class components have just one state variable, an object with multiple keys
  * Function components split up the state into multiple variables, each managed with `useState`


## Guided Project - shopping list app
1. Explore the architecture of our shopping list app:
  * `App` and `ListForm` are class components
  * `Item` and `GroceryList` are function components
  
2. Build state into `App.js`
Write a constructor for the App component
  * super()
  * intialize the component state with grocery data

3. Class properties
  * implement `toggleItem`
  * pass down to `GroceryList` and `Item`
  * add a click handler in `Item` to call your `toggleItem` function
  * remember to start slow and handle architecture first -- you can sipmly pass a dummy function with a `console.log` first to make sure everything is connected right before implementing the actual logic.
  * Binding and synthetic events

4. Implement the logic to update state in `toggleItem`


## Helpful Resources
[Using arrow functions to avoid binding `this` in React](https://medium.com/@joespinelli_6190/using-arrow-functions-to-avoid-binding-this-in-react-5d7402eec64)



  
