# Developer workflow

This guide tries to define an effective workflow for software development. 
It makes use o TDD and Trunk-based development.

## Premisses
* To be able to quickly deviler well tested code, adopt small tasks.
* 

## Workflow

### To do

Work that has not been started. Start by writing tests for the feature you are about to implement. See the [testing section](#testing)

### In progress

Work that is actively being looked at by the team. Usually related to a git branch.

### Code review

Step where an engineer's code is reviewed by other software engineer(s) 

### Done

### Awaiting QA

### Ready to merge

# Trunk based development

A source-control branching model, where developers collaborate on code in a single branch called ‘trunk’ *, resist any pressure to create other long-lived development branches by employing documented techniques. They therefore avoid merge hell, do not break the build, and live happily ever after.

## When to use
* When you are just starting up.
* When you need to iterate quickly.
* When you work mostly with senior developers.

## Benefits

* TBD saves you from merge hell.
* TBD supports the best developing practices, including feature planning, committing small changes, and writing backward compatible code.
* TBD creates an opportunity to deploy new features faster than using feature branching.
* In the long-term, small commits could help split your big monolith application into neat services.

# Gitflow

The overall flow of Gitflow is:

A develop branch is created from master
A release branch is created from develop
Feature branches are created from develop
When a feature is complete it is merged into the develop branch
When the release branch is done it is merged into develop and master
If an issue in master is detected a hotfix branch is created from master
Once the hotfix is complete it is merged to both develop and master

## When to use
* When you have a lot of junior developers.
* When you have an established product.

## Testing

How to build a great test suite
To create a great test suite, think smaller and favor fast, focused unit-tests over slow application-wide end-to-end tests.

Say you are implementing the “search” endpoint of the Product resource described earlier. You might write the following tests:

One “acceptance test”, where you start the application, make an HTTP request to search for a given product name, and verify that expected products were returned. This verifies that all parts of the application are correctly wired together.

Few “integration tests” where you invoke ProductController API from JavaScript/TypeScript, talk to a real database, and verify that the queries built by the controller work as expected when executed by the database server.

Many “unit tests” where you test ProductController in isolation and verify that the controller handles all different situations, including error paths and edge cases.

Testing workflow
Here is what your testing workflow might look like:

Write an acceptance test demonstrating the new feature you are going to build. Watch the test fail with a helpful error message. Use this new test as a reminder of what is the scope of your current work. When the new tests passes then you are done.

Think about the different ways how the new feature can be used and pick one that’s most easy to implement. Consider error scenarios and edge cases that you need to handle too. In the example above, where you want to search for products by name, you may start with the case when no product is found.

Write a unit-test for this case and watch it fail with an expected (and helpful) error message. This is the “red” step in Test Driven Development (TDD).

Write a minimal implementation need to make your tests pass. Building up on the example above, let your search method return an empty array. This is the “green” step in TDD.

Review the code you have written so far, and refactor as needed to clean up the design. Don’t forget to keep your test code clean too! This is the “refactor” step in TDD.

Repeat the steps 2-5 until your acceptance test starts passing.

When writing new unit tests, watch out for situations where your tests are asserting on how the tested objects interacted with the mocked dependencies, while making implicit assumptions about what is the correct usage of the dependencies. This may indicate that you should add an integration test in addition to a unit test.

For example, when writing a unit test to verify that the search endpoint is building a correct database query, you would usually assert that the controller invoked the model repository method with an expected query. While this gives us confidence about the way the controller is building queries, it does not tell us whether such queries will actually work when they are executed by the database server. An integration test is needed here.

To summarize:

Pay attention to your test code. It’s as important as the “real” code you are shipping to production.
Prefer fast and focused unit tests over slow app-wide end-to-end tests.
Watch out for integration points that are not covered by unit-tests and add integration tests to verify your units work well together.


---------------------
Remember to follow the best practices from Data handling when setting up your database for tests:
Integration tests are one of the places to put the best practices in Data handling to work:

Clean the database before each test
Use test data builders
Avoid sharing the same data for multiple tests

----------------------

The TDD process consists of the following steps:

### Start by writing a test
* Run the test and any other tests. At this point, your newly added test should fail. If it doesn’t fail here, it might not be testing the right thing and thus has a bug in it.
* Write the minimum amount of code required to make the test pass
* Run the tests to check the new test passes
* Optionally refactor your code
* Repeat from 1

Unit Testing gives you the what. Test-Driven Development gives you the when. Behavior Driven-Development gives you the how. Although you can use each individually, you should combine them for best results as they complement each other very nicely.

To summarize:

Pay attention to your test code. It’s as important as the “real” code you are shipping to production.
Prefer fast and focused unit tests over slow app-wide end-to-end tests.
Watch out for integration points that are not covered by unit-tests and add integration tests to verify your units work well together.
