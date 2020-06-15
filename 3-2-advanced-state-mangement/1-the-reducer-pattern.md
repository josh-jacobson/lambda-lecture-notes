# The Reducer Pattern

## Key Questions
Think about these main ideas 

## Immutability 

## Data types and pointers in JavaScript
In Javascript, there are six "primitive data types" (`Number, String, BigInt, Symbol, Boolean, undefined`), each of which stores a value of a fixed size in memory. For example, a Number type is always exactly 8 bytes of data, to store a 64-bit floating point value.

How big is an array or object though? These more advanced data structures can be of any size, and require a more complicated system of memory allocation and management. So an Object actually stores a "pointer" to another memory location, where the right amount of storage space can be dynamically allocated.

This is why `Object` in Javascript is known as a "reference type" rather than a "primitive type". For reference types we store a pointer to another memory location rather than storing a fixed amount of data directly. Since all non-primitive data structures (including Array and the mutable String object) inherit from this same Object prototype in JavaScript, we're actually always working with pointers. 

That may all be a bit abstract at first, so here's how it applies in practice:

```javascript
// Copying objects this way just duplicates the pointer, not the object itself
// This leads to unintended side effects! 
const obj = {name: "josh", color: "blue"};
const obj_two = obj;
obj_two.color = "red";
console.log(obj, obj_two); // both have color: red

// That's why we create a new object every time, like this:
const josh = {name: "josh", color: "blue"};
const josh_two = {...josh, color: "red"};
console.log(josh, josh_two); // different colors
```
Because of the way we copied with =, obj and obj_two are pointers to the same object!! Equals assign does not create a new object. Be very careful with this and be aware of what’s going on.

I's possible to create some unexpected side effects when working with these data structures if we aren't careful! In order to keep state changes and their effects throughtout the application **predictable**, we follow the convention of **immutable state** by creating an entirely new object with every state change. Note how the spread operator `...` helps streamline the syntax for this.

We've been following this convention all aong, but it becomes especially important once we start managing application state with Redux and Context API. 

## Helpful Resources:
* [JavaScript data types - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
* [Primitive vs Reference Values](https://www.javascripttutorial.net/javascript-primitive-vs-reference-values/)
