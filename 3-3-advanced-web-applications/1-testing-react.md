# Testing React

## Objectives
* test React components as the props change
* use mocks in web application tests
* test asynchronous API calls that are made in a component

## Review: Why Test?
* Having a comprehensive test suite allows us to trust the code
* Safety net for future changes & refactoring (especially helpful for team collaboration)
* Bugs will immediately be surfaced in the future
* Encourages modular, easy-to understand-code (tangled code is also often difficult to test!)
* Helpful in quality control and deployment
* Tests also act as a form of documentation and enforces best practices
* ...and many other reasons. (*Not testing* is a bad idea, like taking out a high-interest loan of technical debt)

## Review: AAA and test categories 
AAA flow of testing:
* Arrange
* Act
* Assert

And the three most common types of automated tests you'll use: 
![Testing pyramid](images/testing_pyramid.png)

* **End to End testing:** simulating an entire user flow from start to finish. If you're writing an e-commerce app, that flow could be placing items in the cart and completing a purchase. Think of hiring a QA person to go through that whole process and try every edge case they can think of to see if anything breaks. But your QA person is actually a robot. You've seen this before with **Enzyme**
* **Integration testing:** verifying the functionality of a complete piece of application behavior, agnostic of its implementation details. This is similar to E2E but generally focused on more discrete behavior rather than the big picture. For example, an integration test in your e-commerce app might just verify the behavior of adding an item to your cart rather than simulating an entire purchase flow from start to finish. 
* **Unit testing:** verifying that an individual function or component of your application works as expected

Higher-level tests (integration and E2E) take longer to run, are more complex and "expensive". But they also provide the most reliable coverage since they test the actual behavior from a user's perspective rather than the implementation details. 

## Integration Testing with React Testing Library and Jest
Today we'll be focusing on integration testing for React applications, using Jest with React Testing Library.

Here's some new terminology:
* To isolate the behavior of the component we want to test, we can replace other objects and dependencies with **mocks** that simulate the behavior of the real objects. (Entire functions and even external node modules can be mocked too!)
* **Spies** help us verify that the things we expect to be called are actually called, in the order we’d expect. 

The main idea to remember with these more advanced testing concepts is that we want to be specific about what we test.

## Helpful Resources
* [Write tests. Not too many. Mostly integration.](https://kentcdodds.com/blog/write-tests)
* [How to Use React Testing Library](https://www.robinwieruch.de/react-testing-library)
* [Understanding Jest Mocks](https://medium.com/@rickhanlonii/understanding-jest-mocks-f0046c68e53c)
* [React Testing Library cheatsheet](https://testing-library.com/docs/react-testing-library/cheatsheet)
* [Jest Cheat sheet](https://github.com/sapegin/jest-cheat-sheet/blob/master/Readme.md)
* [Previous testing lecture - more links & notes](https://github.com/josh-jacobson/lambda-lecture-notes/blob/master/3-1-advanced-react/4-testing-web-applications.md)
