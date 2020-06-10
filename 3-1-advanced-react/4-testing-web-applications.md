# Testing Web Applications

## Why Test?
* Having a comprehensive test suite allows us to trust the code
* Safety net for future changes & refactoring, very helpful for team collaboration
* Bugs will immediately be surfaced in the future
* Encourages modular, easy-to understand-code (tangled code is also often difficult to test!)
* Helpful in quality control and deployment, particularly in large team contexts
* Tests also act as a form of documentation and enforces best practices
* ...and many other reasons. (*Not testing* is a bad idea, like taking out a high-interest loan of technical debt)

## Four Kinds of Tests
There's a lot of different terminology floating around, and sometimes the categories overlap but here's a relatively easy way to understand the main categories of automated tests. (Kent C. Dodds explains ths really nicely -- check out his article and pdf's below!)

* **End to End testing:** simulating an entire user flow from start to finish. If you're writing an e-commerce app, that flow could be placing items in the cart and completing a purchase. Think of hiring a QA person to go through that whole process and try every edge case they can think of to see if anything breaks. But your QA person is actually a robot. You've seen this before with **Enzyme**
* **Integration testing:** verifying the functionality of a complete piece of application behavior, agnostic of its implementation details. This is similar to E2E but generally focused on more discrete behavior rather than the big picture. For example, an integration test in your e-commerce app might just verify the behavior of adding an item to your cart rather than simulating an entire purchase flow from start to finish. 
* **Unit testing:** verifying that an individual function or component of your application works as expected
* **Static testing:** catch errors and typos in code. (Code linters like ESLint help you with this)

As you might expect, higher-level tests (especially E2E) run a lot slower and have more potential failure points since they test many components at once, as well as the interaction between components. However, these tests are closest to the way your software is actually going to be used, so they provide the most confidence. So you'll start to see that architecture and design decisions are just as important in your automated test suite as in your application code! 

We're basically writing software to test the software, and in large production applications this is incredibly important. There's no one "right way", so your job is to know the tradeoffs and write tests in a way that works best for your specific project. In practice we end up creating a kind of hierarchy or "testing pyramid", where simple concerns are handled with quick unit tests while broader application behavior is ensured with integration and E2E tests.

## Basics of automated testing
AAA flow of testing:
* Arrange
* Act
* Assert

## Unit Testing with Jest
Unit tests are for the individual "units" of your application -- functions, event handlers, and small components.

Jest is a testing framework developed by Facebook. We'll be starting with Jest on its own for unit tests in this lecture, then we'll also see how Jest works together with a DOM testing utility library (RTL is most popular at the moment) for integration testing.

## Integration Testing with React Testing Library and Jest
Here's a nice overview of the integration testing concept from the React Testing Library docs:
> You want to write maintainable tests for your React components. As a part of this goal, you want your tests to avoid including implementation details of your components and rather focus on making your tests give you the confidence for which they are intended. As part of this, you want your testbase to be maintainable in the long run so refactors of your components (changes to implementation but not functionality) don't break your tests and slow you and your team down.

So integration testing is a higher-level form of testing, in which we actually interact with the interface in the same way a user does. While unit tests verify your specific implementation, integration tests are more concerned with the overall *behavior* of your application. With this kind of testing, you could potentially change the details of an implementation and significantly refactor individual functions and components without failing integration tests, as long as the overall behavior is the same.

As an example to understand the difference, for a basic form component you'd have unit tests for each method (`handleChanges`, `submitForm`, etc) and an integration test to verify the overall behavior of a certain action that involves multiple components.

React Testing Library is just a lightweight library that provides some additional utilitiy functions, extending the functionality of `react-dom` and `react-dom/test-utils`. It's intended as a replacement for Enzyme (a testing library developed by engineers at Airbnb, released in 2016 and popular until recently). Note that RTL itself is **not a test runner or framework** -- it's just a library that you can use *with* a testing framework like Jest. Jest + RTL is a popular combination, and we'll be working with this stack to learn some testing basics.

## PDF's to download
* ["What Should I Test?" by Kent C Dodds](pdf/Print_Worksheet_US.pdf)
* [How to Win at JavaScript Testing](pdf/Print_Trophy_US.pdf)
* [Testing Glossary](pdf/Print_Glossary_US.pdf)
* [RTL Cheat Sheet](pdf/RTL_cheat_sheet.pdf)

## Other Helpful Resources
* [Static vs Unit vs Integration vs E2E Testing](https://kentcdodds.com/blog/unit-vs-integration-vs-e2e-tests)
* [Jest API](https://jestjs.io/docs/en/api)
* [RTL Docs](https://testing-library.com/docs/react-testing-library/intro)
* [Arrange, Act, Assert](https://defragdev.com/blog/?p=783)
* [Avoid Nesting When You're Testing](https://kentcdodds.com/blog/avoid-nesting-when-youre-testing)
* [Jest, Enzyme, RTL and Cypress compared](https://medium.com/javascript-in-plain-english/i-tested-a-react-app-with-jest-testing-library-and-cypress-here-are-the-differences-3192eae03850#:~:text=A%20key%20difference%20I%20should,%2DEnd%20(e2e)%20testing.)
