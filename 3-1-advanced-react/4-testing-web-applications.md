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
Integration testing is a higher-level form of testing, generally testing the interface the same way a user would. So we actually rener simulating a complete action (e.g., submitting a form) and ensuring that the result is as expected. While unit tests verify your specific implementation, integration tests are more concerned with the overall *behavior* of your application. Depending on how your tests are structured, you could potentially change the details of an implementation without failing integraiton tests, as long as the overall behavior is the same.

As an example to understand the difference, for a basic form component you'd have unit tests for each method (`handleChanges`, `submitForm`, etc) and an integration test to verify the overall behavior of the form from a user's perspective.

React Testing Library is a lightweight library that provides some additional utilitiy functions to extend the functionality of `react-dom` and `react-dom/test-utils`. It's intended as a replacement for Enzyme (a testing library developed by engineers at Airbnb, released in 2016 and popular until recently).

Here's how the RTL docs explain the problem this library solves:
> You want to write maintainable tests for your React components. As a part of this goal, you want your tests to avoid including implementation details of your components and rather focus on making your tests give you the confidence for which they are intended. As part of this, you want your testbase to be maintainable in the long run so refactors of your components (changes to implementation but not functionality) don't break your tests and slow you and your team down.

## PDF's to download
* ["What Should I Test?" by Kent C Dodds](pdf/Print_Worksheet_US.pdf)
* [How to Win at JavaScript Testing](pdf/Print_Trophy_US.pdf)
* [Testing Glossary](pdf/Print_Glossary_US.pdf)
* [RTL Cheat Sheet](pdf/RTL_cheat_sheet.pdf)

## Other Helpful Resources
* [Jest API](https://jestjs.io/docs/en/api)
* [RTL Docs](https://testing-library.com/docs/react-testing-library/intro)
* [Arrange, Act, Assert](https://defragdev.com/blog/?p=783)
