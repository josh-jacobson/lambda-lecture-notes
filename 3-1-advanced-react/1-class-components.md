# Class Components 
🎓🎓🎓

## Objectives
* Explain class components, and use a class component to render some state data to the DOM
* Share data between components using state and props
* Respond to events triggered by user interaction and handle user input via forms in React
* Understand the foundations of React by seeing how things work "under the hood", before Hooks simplified the interface for developers
* (looking ahead to the next sprint) Start getting comfortable with "component-level" vs "application-level" state

## Intro: OOP vs Functional Programming 😺

Broadly speaking, the two most popular software development styles are object-oriented programming (OOP) and functional programming.

In OOP, programmers design their own advanced data structures called "classes", often to model something in the real world. At my first summer internship at Shmoop, I wrote very cheesy examples of simple classes written in Java for their AP computer science curriculum. For example, an `Animal` class has instance methods `sleep()`, `eat()` and `play()`. We can define a "child class" like `Dog` 🐕 or `Bear` 🐻 to **inherit** the basic functionality of an `Animal` and add some more specific behavior. Maybe `Dog` adds a `cuddle()` method and `Bear` knows how to `maulCarWindowsForPeanutButterSnack()`. In OOP parlance, the blueprint for each kind of animal is called a "class" and each individual is called an "object". When we "instantiate" a new object, it's like birthing a new animal with all the abilities specified by its class.

In old-school React, the parent `Animal` class" is `React.Component` and it has some built-in methods that are quite useful in component-land. We `extend` that class to create a "class component" in its image, inheriting the basics and adding our own useful functions and state.

Functional programming is decidedly less cuddly and a bit harder to wrap our minds around at first. Functions, rather than objects, are the fundamental building blocks of advanced programs. We build from those functional building blocks using composition and currying rather than inheritance.

## OOP and FP in JavaScript

Believe it or not, you already have quite a bit of practice with both styles! JavaScript allows both, kinda. A truly OOP language implements a rigorous class-based inheritance system. Meanwhile, a truly functional programming language (e.g., Elm, Elixir, Erlang) has immutable data types and specific requirements around what a function can and cannot do (namely, no "side effects" for pure functions). 

JavaScript, however, does none of these things and is a bit more of a "choose your own adventure experience". Rather than true classes, JavaScript has a simpler protoype-based inherance model (more on that below) and the ES6 `class` syntax is just syntactic sugar rather than the real thing. Unlike functional languages, Javascript only enforces immutability for simple primitive types, and is extremely loosey-goosey about everything else. The `const` keyword does nothing to enforce immutability for the actual data structures we use every day (objects, arrays, etc). 

Despite the challenges presented by these quirks of the language, JavaScript has come into its own as a powerful and widely used language, allowing some version of both major paradigms for developers with different preferences. In React, we can choose to write OOP-style "class components" based on the ES6 class syntax, or we can use the newer "function component" style.

OOP-style programming in JavaScript was trendy when React came out, hence the class component interface. But the times are a-changin! Now classes are old school, and functional programming is the hot new thing. In a nutshell, that shift in trends is really the reason behind the transition from class components to function components.


## So, are class components still relevant? 🐢

Function components were originally limited in their abilities, but React 16.8 introduced Hooks, allowing function components to "hook into" state and side effects without the need for class components.

Hooks streamline things a lot, and most developers prefer writing new components this way. But you'll also learn something new about the philosophy and principles behind React by learning the "old way" with class components.

And in the real world, you'll usually encounter applications with a mix of class and function components, so it'll help a lot in your career to fully understand both styles.

## Class components 🚂 vs Function components 🚝:
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


## Bonus: ES6 classes and function prototypes in JavaScript 🤓

A good random fact to know for your coding interviews is that Javascript is built on "prototype-based inheritance", a simpler version of the traditional class-based inheritance found in other languages like Java and C++. Though we're now used to seeing `class` terminology used in newer ES6 syntax, Javascript does handle things a bit differently under the hood, and it's worth understanding the differences. 

ES6 has (arguably) changed things for the better, allowing inheritance without having to write a lot of messy, potentially confusing code. You'll almost always end up just writing ES6 classes because they're nicer and easier to understand, but just remember that your ES6 code compiles down to vanilla Javascript and it's the same prototype-based inheritance model at play. Let's take a look at how object-oriented programming works in JavaScript with and without ES6 classes, and try to demystify thigs a bit.

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

ES6 provides a syntax for OOP-style programming that is more familiar to software developers from more traditional object-oriented languages (e.g., C++, Python, Ruby), but at the end of the day it's only "syntactic sugar". The nuts and bolts of the language aren't changed by this newer syntax, and JavaScript's inheritance model is still based on prototypes and constructor functions rather than actual classes.

In other languages, a class constructor creates an instance of the class, but a constructor in JavaScript is simply a function that returns an object. You've seen constructors like `String`, `Array` and `Object` that are built into JavaScript and we've also defined our own. The subtle differences between true class-based OOP and what we do in JavaScript won't make much difference for our purposes in React, but just know that Babel compiles your ES6 `class` down to a constructor function and definitions on its prototype.

In React, when we define a class component that `extends React.Component` we're basically just taking that pre-defined base component class and extending it with our own custom behavior.



## Helpful Resources
[How ES6 classes really work](https://medium.com/@robertgrosse/how-es6-classes-really-work-and-how-to-build-your-own-fd6085eb326a)

[Using arrow functions to avoid binding `this` in React](https://medium.com/@joespinelli_6190/using-arrow-functions-to-avoid-binding-this-in-react-5d7402eec64)

[React.Component documentation](https://reactjs.org/docs/react-component.html)

[State and Lifecycle](https://reactjs.org/docs/state-and-lifecycle.html)

  
