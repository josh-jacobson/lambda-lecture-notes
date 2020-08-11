# Composing and Sharing Non-Visual Behavior

## Custom Hooks 🤠
We all love the convenient interface of `useState` and `useEffect`. We'll also be working with `useReducer` a lot later on in this unit. Sometimes when you're building an app, you'll come up with a clever implementation that is helpful in a lot of different contexts rather than just in the component you're working on at the moment! You can actually just write your own hook to extend the functionality of the hooks built into React. Just like a helper function you'd write to share some functionality across your app, but with React flavor.

Sounds a bit complicated, but it's actually super easy in practice. From the React docs:
> A custom Hook is a JavaScript function whose name starts with ”use” and that may call other Hooks.

Here are some examples of real custom hooks you'll see in the wild:
* useLocalStorage: just like useState, but persist the values to localStorage in case a session is interrupted (we'll build a version of this today)
* useHistory and useParams: nice custom hooks included in React Router for accessing url params and browser history
* useSpeechSynthesis: easy text-to-sound synthesis for your React app (part of `react-speech-kit`)

## Stateful logic and non-visual behavior 👩‍💻
When we talk about "stateful logic" and "non-visual behavior" in React, we're simply referring to all of the logic in a component other than the basics. These are all part of the "stateful logic" in a component:
* Updating state
* Handling form inputs
* Responding to events 

Rendering something to the DOM is an example of basic behavior that is *not* considered "stateful logic". We can write a simple function component that acts as a templating engine, taking a few inputs and formatting them to look nice on the page. A component like that has no "stateful logic".

On a high level, we can simply think about stateful logic as the stuff we do with `useState` and non-visual behavior as the stuff we do with `useEffect`.

(No class components in this lecture, but the same ideas apply there too! In class components, your stateful logic will include `this.setState` calls, and non-visual behavior like event listeners and api calls will happen in the lifecycle methods.)

## Local Storage 🤖
In today's guided project we'll be persisting data to the browser to improve the user experience. One very straightforward way to do this is with the localStorage api, which basically just saves key/value pairs locally in the browser. Here's `localStorage` in a nutshell: 

```javascript
localStorage.setItem('key', 'value');
localStorage.getItem('key'); // returns 'value
```

Along with `localStorage.removeItem` and `localStorage.clear()` for cleanup, that's basically the entire API! Nice and simple. 


## Functional Programming 🤯
Today we'll be "composing" functions and building our own custom hooks. Pretty trendy sounding, but what does *function composition* really mean?

In building custom hooks, we're writing functions that accept functions as their inputs and also return other functions as outputs. "Functional programming" is a whole paradigm (just like object-oriented programming and other styles) but on a basic level it's really just about this clever way of building useful abstractions by allowing functions to receive, call, and return other functions. 

This is all possible because functions are treated as "first-class objects" in JavaScript, meaning that they can be passed around as arguments, assigned to variables, and returned by other functions. Not every programming language is like this! It's a helpful feature of JavaScript that functions are just another type of object inheriting from the same Object prototype.

All of this allows for some pretty powerful programming paradigms, many of which we've already seen in React. So if "functional programming" and "function composition" sound overly complex just realize that you've already worked with these paradigms before and you'll only continue to get more and more comfortable with it as we explore advanced techniques in React.

(Side note: the [λ calculus](https://personal.utdallas.edu/~gupta/courses/apl/lambda.pdf) is a mathematical system underpinning functional programming. Perhaps this is how Lambda School got its name?)


## Helpful Resources:
[Building Your Own Hooks](https://reactjs.org/docs/hooks-custom.html)

[Function composition in computer science](https://en.wikipedia.org/wiki/Function_composition_(computer_science))

[Function composition example in Sonic Pi](https://github.com/josh-jacobson/sonic-pi/blob/master/jj-functional-composition-example.rb)
