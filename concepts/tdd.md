# Test-Driven Development (TDD)
# Test-Driven Development (TDD)

## References
- [TDD Practices](https://app.pluralsight.com/player?course=test-driven-development-java&author=mike-nolan&name=test-driven-development-java-m1&clip=0&mode=live)

## Ideas
Write tests alongside code, not afterwards
Forces you to create code that can be tested, simpler, more modular
Better estimation of remaining progress

Grants ability to refactor code easily

Red / Green / Refactor 
   - Write a test for new function, incompatible with code
   - Write code to pass the test
   - Refactor

Class-Under-Test - unit test should focus on testing methods of a single class, can have multiple test classes to test a single class

Method-under-test - a unit test should exercise a single method to verify logic, assumptions, etc. of that function.

Test fixture/harness - setup of test environment before each test and tear down at end

Mockito - when testing a single method, you want to isolate the functionality, not worrying about dependencies, Mockito lets you mock the dependencies to 

DBUnit - validating data manipulations in DAO

JUnit - java framework for writing unit tests to exercise the functionality within a class

Test has 4 steps
1. Setup - setup dependencies or data
2. Execution - run the tested unit of code
3. Verification - assert that input and output correlate expectedly
4. Teardown - clear data and fixtures created during test

Example: Enable/disable search
  1. Problem statement: 
  "I need to be able to enable/disable automated searching for events like bulk updates"
  2. Break it down into constituent tasks, create in rally
  "I need a way to set enabled/disabled status"
  "I need the service to not run if disabled"
  "I need the service to remember enabled/disabled status"
  3. Explore how the different pieces work, establish cases
  "I need a way to set enabled/disabled status" - endpoint that sets an internal variable
  "I need the service to not run if disabled" - check internal variable before running
  "I need the service to remember enabled/disabled status" - save value in S3, query if state is unknown
  4. Pick a piece, and write the tests"I need the service to not run if disabled" 
     1. Service disabled - don't run
     2. Service enabled - do run
  5. Write the code

## Good Practices

- Well named
   - Provides documentation on behavior of code
   - Should be able to go from test name to body of code easily
   - Name reflects what is being tested
   - Use domain language, natural language, and be descriptive
- Test behavior, not implementation
      - Only focus on public behavior - think "no trespassing" into class
- DRY - Don't repeat yourself
- Diagnostics
