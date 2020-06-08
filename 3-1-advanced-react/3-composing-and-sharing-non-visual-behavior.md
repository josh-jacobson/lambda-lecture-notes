# Composing and Sharing Non-Visual Behavior

## Review: Stateful Logic and Non-visual behavior
When we talk about "stateful logic" and "non-visual behavior" in React, we're simply referring to all of the logic in components apart from the basics like rendering stuff to the DOM. Updating state, handling form inputs and responding to events are all part of this "stateful logic".

## Functional Programming
You may notice that in building custom hooks, we're creating many layers of abstraction with functions that accept functions as their inputs and also return other functions as outputs. All of this function composition may seem very confusing at first, but don't let it intimidate you! Functions are just a type of object in JavaScript, inheriting from the Object prototype. And they're treated as "first-class objects" in JavaScript, meaning that they can be passed around as arguments, assigned to variables, and returned by other functions. 

All of this allows for some pretty powerful programming paradigms, many of which we've already seen in React! So if functional programming sounds complex just realize that you've already done a lot of it and you'll only continue to get more and more comfortable with it as we explore advanced programming techniques with React.

(Side note: the [λ calculus](https://personal.utdallas.edu/~gupta/courses/apl/lambda.pdf) is a mathematical system underpinning functional programming, and one can only wonder if this is where Lambda School got its name?)


## Helpful Resources:
[Building Your Own Hooks](https://reactjs.org/docs/hooks-custom.html)
