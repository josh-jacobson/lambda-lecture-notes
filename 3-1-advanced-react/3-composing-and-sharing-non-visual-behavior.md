# Composing and Sharing Non-Visual Behavior

## Review: Stateful Logic and non-visual behavior
When we talk about "stateful logic" and "non-visual behavior" in React, we're simply referring to all of the logic in a component other than the basics. These are all part of the "stateful logic" in a component:
* Updating state
* Handling form inputs
* Responding to events 

Rendering something to the DOM is an example of basic behavior that is not considered "stateful logic". We can write a simple function component that acts as a templating engine, taking a few inputs and formatting them to look nice on the page. A component like that has no "stateful logic".

On a high level, we can simply think about stateful logic as the stuff we do with `useState` and non-visual behavior as the stuff we do with `useEffect`.

We won't be working with class components in this lecture, but the same ideas apply. Your stateful logic will include `this.setState` calls, and non-visual behavior like event listeners and api calls will happen in the lifecycle methods.

## Functional Programming
In this lecture we'll be composing functions and building our own custom hooks.

You may notice that in building custom hooks, we're creating many layers of abstraction with functions that accept functions as their inputs and also return other functions as outputs. All of this may seem very confusing at first, but don't let it intimidate you! 

Functions are just a type of object in JavaScript, inheriting from the same Object prototype. And they're treated as "first-class objects" in JavaScript, meaning that they can be passed around as arguments, assigned to variables, and returned by other functions. 

All of this allows for some pretty powerful programming paradigms, many of which we've already seen in React! So if functional programming sounds complex just realize that you've already done a lot of it and you'll only continue to get more and more comfortable with it as we explore advanced programming techniques with React.

(Side note: the [λ calculus](https://personal.utdallas.edu/~gupta/courses/apl/lambda.pdf) is a mathematical system underpinning functional programming. Perhaps this is how Lambda School got its name!)


## Helpful Resources:
[Building Your Own Hooks](https://reactjs.org/docs/hooks-custom.html)

[Function composition in computer science](https://en.wikipedia.org/wiki/Function_composition_(computer_science))

[Function composition example in Sonic Pi](https://github.com/josh-jacobson/sonic-pi/blob/master/jj-functional-composition-example.rb)
