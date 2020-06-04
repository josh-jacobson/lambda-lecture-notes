# The React Lifecycle

## Review: Class Components

Here's the basic format you'll use when writing class components in React:

```javascript
class Lambda extends React.Component {
  constructor() {
    super(); // calls the constructor from React.Component, which intializes this.props
    // initialize state here
  }
  
  // lifecycle methods: componentDidMount, componentDidUpdate, componentWillUnmount, etc.
  
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

export default Lambda;
```

## What are lifecycle methods? 

This may feel a bit complex at first, especially coming from the more streamlined Hooks approach. An easy way to understand the React lifecycle is that it's simply “when a component does what it does, and why". 

Just like a 🌿 or 🦔, a React component has three phases to its "lifecycle", and different things need to happen at each stage of life:
* Birth / mounting (`componentDidMount`)
* Growth / updating (`componentDidUpdate`)
* Death / unmounting (`componentWillUnmount`)

Sometimes they even render child components 🐣 too! But I may be overextending a questionable metaphor. Moving on...

## `render()`
Should be a pure function, meaning that it:
* does not modify component state 
* returns the same result each time it’s invoked
* does not directly interact with the browser.

If you were to implement the same component as a function and as a class, the JSX returned from `render()` is the same as what you return from the function component itself. 

## constructor()
For React class components, constructors are only used for two purposes:
* Initializing local state by assigning an object to `this.state`
* Binding event handler methods to an instance.

If you don’t initialize state and you don’t bind methods, you don’t need to implement a constructor for your React component. Remember that the `super()` call will happen even if you don't write a constructor.

For initialization, in the constructor we assign `this.state` directly. This is the only place we ever do this! In all other methods, use `this.setState()`. 

## Common lifecycle methods: `componentDidMount`, `componentDidUpdate` and `componentWillUnmount`
Together, these three lifecycle methods are roughly equivalent to the `useEffect()` hook.

Use these to setup listeners, fetching data from an API and ultimately removing listeners before component is removed ("unmounted") from the DOM.

These are the lifecycle methods you'll use often

## Rarely used lifecycle methods:
* getDerivedStateFromProps
* shouldComponentUpdate
* getSnapshotBeforeUpdate

And some others that are deprecated now. Focus on just getting really comfortable with the 3 above, as you'll mainly just see those in most cases. If you're curious about learning all of these though, just take a few minutes for a full read of the API reference below.

## Helpful Resources
[React.Component lifecycle methods - API reference](https://reactjs.org/docs/react-component.html) 

[Lifecycle method diagram](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

[React component’s lifecycle - Medium article](https://medium.com/react-ecosystem/react-components-lifecycle-ce09239010df)


