# Context API

The React Context API allows you to easily access data at different levels of a component tree, without having to pass data down through props.

## Objectives
* Describe what the Context API is and the problem is solves
* Provide data to the component tree with a context provider
* Consume data from a context object in nested components

## A hierarchy of state management
You'll hear about these three main "levels" of state:
* Application-level state
* Context-level state
* Component-level state

## When to use Context
* Context is designed to share data that can be considered “global” among a tree of React components. This component tree doesn't necessarily meed to be your entire application, it could be just a subtree of components dealing with user login or another applicatoin concern where it's helpful to manage state above the individual component level.

## Provider and Consumer
The setup of Context API is similar to Redux, just simpler. First we create a context (just like creating a store in Redux), and wrap our components with a Provider:
```javascript
const AppContext = React.createContext();
export const Provider = AppContext.Provider;

function App(){
    return (
        <Provider value={value}>
            <ChildComponent />
        </Provider>
    )
}
```

Rather than `connect`ing components, React's Context API uses a more straightforward pattern of provider and consumer. We can either wrap our view logic with a `Consumer` or make things easier by using the `useContext` hook. Here are two ways to consume a context:
```javascript
// First way: wrap with Consumer
// render props pattern (aka ‘function as a child’)
const Component = () => {
  return (
      <AppContext.Consumer>
        {value => (
            <div>{value}</div>
        )}
      </ApContext.Consumer>
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
<button onclick={() => dispatch({type: 'ACTION_TYPE'})>Update</button>
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
