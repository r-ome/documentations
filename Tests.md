## Tests
---
## Kinds of testing

### **Blackbox testing**
  - **WHAT**
    - a testing approach where knowledge of the internal structure of the program is unknown to the tester
    - AKA data-driven, box testing, **functional** testing
    - focuses on external expectations
    - ideal for higher levels of testings
    - testers will only know about the input and the expected output
    - less exhaustive and time-consuming
  - **PROs**
    - unbiased tests because the designer and tester work independently
    - testers can be non-technical
    - test is performed from a user's point-of-view and not the designer's
    - test cases can be designed immediately after the completion of specs
  - **CONs**
    - tests can be redundant
    - test cases are extremely difficult to be designed without clear and concise specs
    - it is difficult to identify *all* possible inputs in limited testing time. Time consuming.
    - there is a high probabilty of repeating tests already performed by the programmer
    - cannot be used for testing complex segments of code
  - **WHEN**
    - Upon integration, system and acceptance testing
  - **WHY**
    - asks the questions
      - *"What happens when a user tries to do that?"*
      - *"Does it really work?"*
    - attempts to find:
      - incorrect or missing functions
      - interface errors
      - errors in data structures
      - behavior or performance errors
      - initialization and termination errors
  - **HOW**
    - Techniques
      - Equivalence Partition
        - technique that involves dividing input values into valid and invalid partitions and selecting representative values from each partition as test data
        - test partition once (the assumption is that any input within a parition is equivalent. i.e. produces the same output)
        - example:
          - an input field that accepts an age of 18 - 56
            |           | Invalid | Valid | Invalid |
            | --------- | ------- | ----- | ------- |
            | Test Case | <=17    | 18-57 | >=57    |
          - an input field that accepts a mobile number with 10 digits
            |           | Invalid     | Valid       | Invalid     |
            | --------- | ----------- | ----------- | ----------- |
            | Test Case | length < 10 | length = 10 | length > 10 |
      - Boundary Value Analysis
        - technique that involves the determination of boundaries for input values and selecting values that are at the boundaries and just inside/outside of the boundaries as test data
        - test **BOTH SIDES** of each boundary (the assumption is that the system behaves differently on either side of a boundary)
        - based on the fact that input values near the boundary have higher chances of error
        - example:
          - an input field that accepts an age of 18 - 56
            |           | BV below the lower boundary | BV above the lower boundary |
            | --------- | --------------------------- | --------------------------- |
            | Test Case | 17                          | 18                          |

            |           | BV below the above boundary | BV above the above boundary |
            | --------- | --------------------------- | --------------------------- |
            | Test Case | 56                          | 57                          |
      - Cause-Effect Graphing
        - technique that involves identifying the cases (input conditions) and effects (output conditions), producing a cause-effect graph, and generating test cases accordingly
  - **Best Practices**
    - Refer to the techniques
### Whitebox testing
  - **WHAT**
    - a testing approach in which internal structure is known to the tester. 
    - AKA structural testing, clear/glass box testing, code-based testing.
    - focuses on the quality of the code
    - ideal for a lower level of testing like unit testing, integration testing
    - easy to automate
    - usually done by testers and developers
    - exhaustive and time-consuming
  - **PROs**
    - code optimization
    - test cases can easily be automated
    - covers all possible paths of a code thereby, empowering a team to conduct thorough application testing
    - programmers introspection
  - **CONs**
    - updated test scripts required when implementation is changing too often
    - some conditions might be untested as it is not realistic to test every single one
    - requires high level knowledge of testers
    - requires code access
  - **WHEN**
    - upon unit testing, integration testing
  - **WHY**
    - test as much code as possible
    - ensure that all independent paths within a module have been exercised at least once.
    - ensures all loops executed at their boundaries and within their operational bounds internal data structures validity
  - **HOW**
    1. understand the code
    2. create test cases
    3. execute
  - **Best Practices**
    - it varies on the testing

---

## Types of testing

### Unit Testing
  - ***What do they test?***
    - evaluates each atomic unit of code the way it's supposed to.
  - ***When do I run them?***
    - should be written and run in parallel with your code.
  - **Why do I need them?**
    - improves code quality
    - finds bugs early
    - provides documentation
    - improves design
    - Automated test
    - inspires confidence
  - **Best Practices**
    - Readable
    - Reliable
    - Fast
    - Simple
  - **Example**
```
// addition.js

export const add = (a, b) => a + b


// addition.test.js
const { add } = require("./addition")

test("should return 5", () => {
    const result = add(2,3);
    const expectedResult = 5;
    expect(result).toBe(expectedResult)
})
```

### Integration Testing
  - ***What do they test?***
    - checks the interaction between two or more atomic units
  - ***When do I run them?***
    - should be the next step after unit tests
  - ***Why do I need them?***
    - makes sure that the software modules work together appropriately
    - ensures that the various modules of the software work in unity
    - verifies the functionality, performance, and reliability between integrated modules.
  - ***How?***
    - Approaches
      - Top Down
          - takes place from top to bottom following the control flow
          - high-level modules are tested first and then low-level modules and finally integrating the low-level modules to high-level
            to ensure the system is working and intended to
            | ADVANTAGES                   | DISADVANTAGES                      |
            | ---------------------------- | ---------------------------------- |
            | extremely consistent         | requires several stubs             |
            | less time required           | poor support for early release     |
            | fault localization is easier | basic functionality is tested late |
            | detects major flaws          |                                    |
      - Bottom Up
          - takes place from bottom of the flow upwards
      
            | ADVANTAGES                           | DISADVANTAGES                           |
            | ------------------------------------ | --------------------------------------- |
            | efficient application                | requires several drivers                |
            | less time required                   | data flow is tested late                |
            | test conditions are easier to create | poor support for early release          |
            |                                      | key interface defects are detected late |
      - Big Bang 
          - all components/modules are integrated simultaneously after which everything is tested as a whole

            | ADVANTAGES                     | DISADVANTAGES                              |
            | ------------------------------ | ------------------------------------------ |
            | all components are tested once | lot of delay before testing                |
            | convinient for small systems   | difficult to trace cause of failures       |
            |                                | possibility of few missing interface links |
            |                                | critical modules are not prioritized       |
      - Sandwich Integration Approach
          - middle layer is the target layer
          - top-down approach is topmost layer
          - bottom-up approach is lowermost layer

            | ADVANTAGES                            | DISADVANTAGES                 |
            | ------------------------------------- | ----------------------------- |
            | both layers can be tested in parallel | High Cost                     |
            |                                       | Big skill set                 |
            |                                       | extensive testing is not done |
    - Steps:
      1. choose the module to be tested
      2. decide the type of integration testing
      3. deploy the selected modules and start testing
      4. perform functional and structural testing
      5. record, analyse and report the results
      6. repeat above steps until complete system is fully tested
      7. deploy for next level testing 
    - Column
      - Test Case ID
      - Test Case Objective
      - Test Case Description
      - Expected Outcome

### Regression Testing
  - ***What do they test?***
    - checks a set of scenarios that worked in the past and should be relatively stable
    - system-wide test that ensures a small change does not break an existing functionality elsewhere in the system
    - all about making sure that all bugs don't come back to haunt you
  - ***When do I run them?***
    - after integration tests pass.
    - do not add new feature to the regression test suite untile existing regression tests pass
  - ***Why do I need them?***
    - it indicates that you have inadvertently reintroduced a bug that you fixed in the past
    - lets you know what old features are broken
    - indicates that a new feature/functionality has broken some existing functionality, causing a regression
  - ***How?***
    - Techniques
      - retesting
        - involves re-execution of all existing and available test suites or cases
      - selective test cases
        - selecting the limited number fo test cases, based on needs and requirements
      - test case prioritization
        - involves priority wise execution of the test cases based on business requirements
    - Columns
      - Test Objective: what are you planning to do
      - Test Object: component to be tested
      - Test Item: subset of test object
      - Test Condition: based on what conditions your test object under which a test item comes
      - Test Case: parameters, test data, preconditions, expected results, actual results
      - Test Suite: collection of test cases

### Smoke Testing
  - ***What do they test?***
    - checks the site's core functionality
  - ***When do I run them?***
    - you should run them early and often, ideally daily, in both staging and production environments
    - done by developers before giving build to testing team
    - done by testers before they start the detailed testing
    - when new features are developed
  - ***Why do I need them?***
    - defects bugs identified at early stages
    - minimizes integration risks
    - saves test effort as test time
  - ***How?***
    - steps
      - deploy the initial builds
      - design test case
      - sizing a smoke test suite
      - automation execution of tests
      - execute tests and generate reports
    - columns
      - test id
      - test scenario
      - description
      - test steps
      - expected results
      - actual results
      - status (PASSED|FAILED)




### User Acceptance Testing (UAT)
  - ***What do they test?***
    - makes sure that the feature as written actually meets all of the initial specification or acceptance criteria
  - ***When do I run them?***
    - comes after system testing
  - ***Why do I need them?***
    - assures the software runs according to the business requirements
    - gives a non-technical perspective
  - ***How?***
    - Planning
      - gathers the acceptance criteria
      - gets the scope (who, communcation, test case result templates)
    - Designing
      - create test cases (acceptance criterias) and test suites
      - and end-to-end nature
    - Execute
      - generates results if (GO or NO GO)
    - QA has different involvements
      - no involvement
      - assist
      : eg. traning
      - full: QA does all the testing
    - if there are bugs
      - go as is
      - defer the issure to a future release
      - delay the deployment date - fix first - severe issues