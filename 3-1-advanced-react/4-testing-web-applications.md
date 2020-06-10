# Testing Web Applications

## Why Test?
* Having a comprehensive test suite allows us to trust the code
* Bugs will immediately be surfaced in the future
* Behavior-driven development (BDD) and similar approaches ensure that your code is modular and easy to understand (since badly convoluted code is also often difficult to test)
* Tests provide a form of reassurance for future developers in the codebase that they're not unknowingly breaking something with their changes
* Helpful in quality control and deployment, particularly in large team contexts
* Tests also act as a form of documentation and help enforce best practices in your code

## Basics of automated testing
AAA flow of testing:
* Arrange
* Act
* Assert

## Unit Testing with Jest
Unit tests are for the individual "units" of your application -- functions, event handlers, and components.

## Integration Testing with React Testing Library
Here's a summary of the idea from the React Testing Library docs:
> You want to write maintainable tests for your React components. As a part of this goal, you want your tests to avoid including implementation details of your components and rather focus on making your tests give you the confidence for which they are intended. As part of this, you want your testbase to be maintainable in the long run so refactors of your components (changes to implementation but not functionality) don't break your tests and slow you and your team down.

So integration testing is a higher-level form of testing, in which we actually interact with the interface in the same way a user does. While unit tests verify your specific implementation, integration tests are more concerned with the overall *behavior* of your application. With this kind of testing, you could potentially change the details of an implementation and significantly refactor individual functions and components without failing integration tests, as long as the overall behavior is the same.

As an example to understand the difference, for a basic form component you'd have unit tests for each method (`handleChanges`, `submitForm`, etc) and an integration test to verify the overall behavior of the form from a user's perspective.

React Testing Library is a lightweight library that provides some additional utilitiy functions to extend the functionality of `react-dom` and `react-dom/test-utils`. It's intended as a replacement for Enzyme (a testing library developed by engineers at Airbnb, released in 2016 and popular until recently). Note that RTL itself is not a test runner or framework -- it's just a library that you can use with any testing framework. At the moment Jest is a popular choice, which is why we'll be learning testing basics with this combination (Jest + RTL). 

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
* [Jest, Enzyme, RTL and Cypress compared](https://medium.com/javascript-in-plain-english/i-tested-a-react-app-with-jest-testing-library-and-cypress-here-are-the-differences-3192eae03850#:~:text=A%20key%20difference%20I%20should,%2DEnd%20(e2e)%20testing.)
