# Context API

The React Context API allows you to easily access data at different levels of a component tree, without having to pass data down through props. 

## A hierarchy of state management
You'll hear about these three main "levels" of state:
* 🌏 Application-level state world
* 🏙️ Context-level state 
* 🏠 Component-level state

The name "Context" in this case just encapsulates the idea that you're defining a subtree of components among which to share state, and you can define the top of that tree wherever you like. Your "context" could be your entire application like it is for Redux, or you could have several different contexts that are each relevant to a "subtree" of your React component tree.

## What is Context API? (and what isn't it?)

Context API takes a more modular approach to state management, providing the storage piece and allowing any number of customized approaches to the rest of the architecture. It's possible to build something that looks like Redux, but there are many other possibilities!

The Redux architecture as we know it can be broken down into these four pieces:
1. Store (a "state container" acting as the single source of truth for shared application state)
2. Reducers to manage state
3. Action creator functions
4. React Redux to connect components to the store: `Provider` plus:
* `connect(mapStateToProps, mapDispatchToProps)` (older HOC syntax)
* `useSelector`, `useDispatch` (new hooks syntax)

Context API just implements #1, a shared store for a component and its children. **A Context is just a shared container, that's it. Unlike Redux, Context API is not a comprehensive state management solution and does not require the use of reducers, actions or action creators.**

## useContext with useReducer
On its own, Context API is *not* a comprehensive application state management system like Redux. However, it's surprisingly powerful! We can also store `dispatch` or setter functions in a Context, allowing components down the tree to not only read, but also update shared state without any need for prop drilling.

Combining the `useContext` and `useReducer` hooks can provide a powerful architecture that is similar to Redux in many ways, and this is becoming increasingly popular as an alternative to Redux due to easier setup and the less opinionated nature of these built-in hooks. But just remember that Context itself is nothing more than a way of sharing state directly from a top level component to any of the child components in its subtree. 

This combination provides a lot of power and predictability for your state mangement, closely modeling the architecture of Redux. All the patterns we've been learning throughout this unit are the same here -- actions, reducers, and a shared state container (context or store). 

The `useContext` & `useReducer` architecture is less opinionated than Redux, and you can choose to add as much abstraction as you'd like but the standard approach is just a bit simpler than Redux. Typically we'll just consume values from the context with `useContext` as shown above, and dispatch actions to update the context with `useReducer`:

```javascript
const [state, dispatch] = useReducer(reducer, initialState);

// within a component:
<button onclick={() => dispatch({type: 'UPDATE_TITLE'})>Update</button>
```

It's up to you to decide whether you'd like to define actions inline like this, or store them in a dedicated file (often a better choice). You could even recreate the action creators pattern and use the same abstractions as Redux, but using an *unopinionated* API like this means that those decisions are left up to you.

## Shared state: three ways to do it
To share state among components, there are really two distinct problems to solve: 
1. Sharing state from a component to its child components (pass values as props)
2. Allowing child components to *update* that top-level state (pass setter functions down as props)

Here are three common approaches that we've now learned: 

### Prop drilling:
1. Pass shared state values down the component tree as props
2. Also pass setter functions (or `dispatch`) as props

### Redux:
1. Provide a store as the single source of the truth for application-level state, and use React Redux to connect componoents to read the values they need from the store with either `mapStateToProps` or `useSelector`
2. Handle all state updates with reducers. Write action creator functions to handle the business logic for each action type, and use `mapDispatchToProps` or `useDispatch` to allow components to dispatch these actions to the reducer.

### Context:
1. Provide a Context (just like a store) to child components, as the single source of the truth for state values relevant to all of those components. Child components can "consume" that context directly to access the values they need, with live updates. 
2. Context doesn't solve this part directly. Choose your own adventure -- common approaches:
    * Pass down setter functions just like you would in a simple non-Redux implementation (prop drilling)
    * Store the setter functions along with state values in the Context to avoid prop-drilling
    * Also add `useReducer` to the implementation and store `dispatch` in the Context (you'll still have to write out each `dispatch` directly, no Redux-style abstraction magic here unless you choose to build it yourself or integrate another library that does so).

## When to use Context
As you can see in the comparison above, React's Context API is more of a simple, modular approach with a very different design philosophy from Redux. It can be used in a variety of ways -- you'll most likely want to centralize all your shared state in a Context, but it's up to you whether you'd like to also store setter functions or `dispatch` in the Context, or just pass those as props when it makes sense. You're always welcome to mix and match, and the interface is also designed with multiple Contexts in mind. 

Rather than a single store with a big branching tree, you can consider each section of your application (auth, user profile, content feed, shop, etc) and create a local Context for each section, sharing state among that subtree of components. Often it makes sense to share state among some components, while simply passing props in another section of the app if there isn't a lot of shared state. The freedom to mix and match is one of the best things about the Context approach.

It's helpful to think of Context API as the "store" part of the architecture, allowing us to share state (and setter functions or dispatch) from the component at the top level of the context tree to any subcomponents that need that data, without having to pass the data through each level of the tree. 

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

## Redux or Context?
Redux is still the standard for managing application-level state in large, complex applications. Context API offers a simpler approach that works well for many smaller applications, with less setup time needed. If current trends continue, Context may grow so much in popularity that it eventually gains more robust functionality and replaces Redux in many large applications. These technologies are always evolving, so for now it's just good to know both and understand the concepts through each lens. A year or two down the road when you may consider the best technology for a new application, everything will be totally different so it's your deep understanding of the concepts and fundamentals that will really allow you to bring valuable insight to your team. 

Here's a quick comparison:
* Context just handles the "store" piece, rather than proivding a comprehensive, opinionated solution for a completely defined architecture like Redux
* You can choose to use Context on its own, or integrate with a number of other frameworks to customize your own solution for state management. A common and powerful combo is `useContext` with `useReducer`, which together provide most of the Redux pattern but with less overhead and more flexibility. 
* Redux is independent of React and can also be used with other frameworks. Context is part of React
* Both allow you to share state between components, but Redux also:
    * comes with a time-traveling debugger
    * provides a middleware API
    * defines a complete architecture pattern
* Setting up Redux: 1) `createStore` 2) wrap entire application with `<Provider>` 3) `connect` components 
* Setting up Context: 1) `createContext` 2) wrap components with `<Provider>` 3) consume with `Context.Consumer` or `useContext`
* Redux is built for large scale, currently used in many massive production apps. Context is newer and may eventually replace Redux for many use cases, but Redux has simply been around longer and is still a good, battle-tested choice for many applications (including those built with frameworks other than React)

## Helpful Resources
* [Context Docs](https://reactjs.org/docs/context.html)
* [Provider Pattern](https://blog.flexiple.com/provider-pattern-with-react-context-api/)
* [How to Use React’s Context API and useContext() Hooks Effectively](https://medium.com/better-programming/how-to-use-reacts-context-api-and-usecontext-hooks-effectively-ed98ad9343b6)
* [How to use the useContext hook in React](https://upmostly.com/tutorials/how-to-use-the-usecontext-hook-in-react)
* [How to use React Context effecively](https://kentcdodds.com/blog/how-to-use-react-context-effectively)
* [You Don’t Even Need React-Redux and Redux Thunk](https://medium.com/better-programming/you-dont-even-need-react-redux-and-redux-thunk-d9dce6c0a89f) - read the bottom section for some useful info!
