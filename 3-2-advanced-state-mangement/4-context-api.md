# Context API

## A hierarchy of state management
You'll hear about these three main "levels" of state:
* Application-level state
* Context-level state
* Component-level state

## When to use Context
* Context is designed to share data that can be considered “global” among a tree of React components. This component tree doesn't necessarily meed to be your entire application, it could be just a subtree of components dealing with user login or another applicatoin concern where it's helpful to manage state above the individual component level.

## Provider and Consumer

## useContext Hook

## Redux or Context?
Redux is still the standard for managing application-level state in large, complex applications. Context API offers a simpler approach that works well for many smaller applications, with less setup time needed. If current trends continue, Context may grow so much in popularity that it eventually gains more robust functionality and replaces Redux in many large applications. These technologies are always evolving, so for now it's just good to know both and understand the concepts through each lens. A year or two down the road when you may consider the best technology for a new application, everything will be totally different so it's your deep understanding of the concepts and fundamentals that will really allow you to bring valuable insight to your team. 

## Helpful Resources
* [Context Docs](https://reactjs.org/docs/context.html)
