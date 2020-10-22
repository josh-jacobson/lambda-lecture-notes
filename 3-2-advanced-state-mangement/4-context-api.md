# Context API

The React Context API allows you to easily access data at different levels of a component tree, without having to pass data down through props. 

## A hierarchy of state management
You'll hear about these three main "levels" of state:
* Application-level state
* Context-level state
* Component-level state

## When to use Context
Context is useful for sharing data that can be considered “global” among a tree of React components, generally a subset of components rather than the entire application. On its own, the Context API simply provies an alternative to prop drilling, and it's helpful to think of it as providing the same behavior. The idea is to share state from the component at the top level of the context tree to any subcomponents that need that data, without having to pass the data through each level of the tree. 

Context API on its own is *not* a comprehensive application state management system like Redux. Combining the `useContext` and `useReducer` hooks can provide a powerful architecture that is similar to Redux in many ways, and this is becoming increasingly popular as an alternative to Redux due to easier setup and the less opinionated nature of these built-in hooks. But just remember that Context itself is nothing more than a way of sharing state directly from a top level component to any of the child components in its subtree. 

Check out the docs (linked below) for a more in-depth understanding of the pros and cons of using Context. There are a few ways of solving this problem of shared state, and you'll find that there are specific tradeoffs involved with each option. Context provides an elegant solution, but baking the state sharing logic into components in this way does make it harder to reuse components.


## Provider and Consumer
The setup of Context API is similar to Redux, just simpler. First we create a context (just like creating a store in Redux), and wrap our components with a Provider:
```javascript
// Calling createContext creates a Provider and a Consumer
const FamilyContext = React.createContext();

function App(){
    return (
        <FamilyContext.Provider value={value}> // the value stored in our context can be any data type -- object, array, string, number, etc.
            <ChildComponent />
        </FamilyContext.Provider>
    )
}
```

Rather than `connect` at the component level, React's Context API uses a more straightforward pattern of provider and consumer. We can either wrap our view logic with a `Consumer` or make things easier by using the `useContext` hook. Here are two ways to consume a context:
```javascript
// First way: wrap with Consumer, render props pattern
const Component = () => {
  return (
      <FamilyContext.Consumer>
        {value => (
            <div>{value}</div>
        )}
      </FamilyContext.Consumer>
  );
};


// Second way (nicer): useContext
function ChildComponent(){
    const contextValue = useContext(AppContext)
    return <div>{contextValue}</div>
}
```

## useContext with useReducer
This combination provides a lot of power and predictability for your state mangement, closely modeling the architecture of Redux. All the patterns we've been learning throughout this unit are the same here -- actions, reducers, and a shared state container (context or store). 

The `useContext` & `useReducer` architecture is less opinionated than Redux, and you can choose to add as much abstraction as you'd like but the standard approach is just a bit simpler than Redux. Typically we'll just consume values from the context with `useContext` as shown above, and dispatch actions to update the context with `useReducer`:

```javascript
const [state, dispatch] = useReducer(reducer, initialState);

// within a component:
<button onclick={() => dispatch({type: 'UPDATE_TITLE'})>Update</button>
```

It's up to you to decide whether you'd like to define actions inline like this, or store them in a dedicated file (usually a better choice). You could even recreate the action creators pattern and use the same abstractions as Redux, but the idea of an *unopinionated* API like this is that those decisions are left up to you.

## Redux or Context?
Redux is still the standard for managing application-level state in large, complex applications. Context API offers a simpler approach that works well for many smaller applications, with less setup time needed. If current trends continue, Context may grow so much in popularity that it eventually gains more robust functionality and replaces Redux in many large applications. These technologies are always evolving, so for now it's just good to know both and understand the concepts through each lens. A year or two down the road when you may consider the best technology for a new application, everything will be totally different so it's your deep understanding of the concepts and fundamentals that will really allow you to bring valuable insight to your team. 

Here's a quick comparison:
* Context API is much less opinionated, can be implemented with a variety of choices rather than having one completely defined architecture
* Redux is independent of React and can also be used with other frameworks. Context is part of React
* Both allow you to share state between components, but Redux also:
    * comes with a time-traveling debugger
    * provides a middleware API
    * defines a complete architecture pattern
* You can use reducers with Context API, but they're not required
* Setting up Redux: 1) `createStore` 2) wrap entire application with `<Provider>` 3) `connect` components 
* Setting up Context: 1) `createContext` 2) wrap components with `<Provider>` 3) consume with `Context.Consumer` or `useContext`
* Redux is built for large scale, currently used in many massive production apps. Context is newer and may eventually replace Redux for many use cases, but Redux has simply been around longer and is still a good, battle-tested choice for many applications (including those built with frameworks other than React)

## Helpful Resources
* [Context Docs](https://reactjs.org/docs/context.html)
* [How to use the useContext hook in React](https://upmostly.com/tutorials/how-to-use-the-usecontext-hook-in-react)
* [How to use React Context effecively](https://kentcdodds.com/blog/how-to-use-react-context-effectively)
* [You Don’t Even Need React-Redux and Redux Thunk](https://medium.com/better-programming/you-dont-even-need-react-redux-and-redux-thunk-d9dce6c0a89f) - read the bottom section for some useful info!
