# Class Components

React development originally focused on class components, written like this:

```javascript
class Lambda extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

The base Component class includes built-in functionality for managing state and other React features. We'll learn about the lifecycle methods of class components in the following lecture.

Function components were originally limited in their abilities, but React 16.8 introduced Hooks, allowing function components to "hook into" state without the need for class components.

Hooks streamline things a lot, and most developers prefer writing new components this way. However, you'll learn about the philosophy and principles behind React by learning the "old way" with class components.

And in the real world, you'll usually encounter applications with a mix of class and function components, so it'll help a lot in your career to understand both approaches.

## Guided Project - shopping list app
1. Explore the architecture of our shopping list app:
  * All class components, except for `Item`
  
Class components vs Function components:
  * In class components we use lifecycle methods to manage state and side effects. For function components we use Hooks.
  * Hooks cannot be used in class components! (and lifecycle methods are not used in function components)
  * Class components have just one state variable, an object with multiple keys
  * Function components split up the state into multiple variables, each managed with `useState`

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

4. 


  
