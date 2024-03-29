`#es6` `jest` `#assembler-institute` `#master-in-software-engineering`

# Assembler Institute: Jest Intro Workshop <!-- omit in toc -->

In this workshop you will learn how to work with Jest for testing javascript applications.

## Table of Contents <!-- omit in toc -->

- [Getting Started](#getting-started)
- [Contents and Branches Naming Strategy](#contents-and-branches-naming-strategy)
- [Workshop Material](#workshop-material)
- [What is Jest?](#what-is-jest)
- [Writing Your First Test](#writing-your-first-test)
- [Jest File Naming Conventions](#jest-file-naming-conventions)
- [Matchers](#matchers)

## Getting Started

First, you will need to clone the repo:

```bash
$ git clone https://github.com/assembler-school/jest-intro-workshop.git
```

Then, you will have to install all the dependencies with npm:

```bash
$ npm install
```

And jest globally so that you can run it from the terminal:

```bash
$ npm install --global jest
```

## Contents and Branches Naming Strategy

The repository is made up of several branches that include the contents and exercises of each section.

The branches follow a naming strategy like the following:

- `{NN}-exercise`: includes the main contents and the instructions of the exercises
- `{NN}-exercise-solution`: includes the solution of the exercises

## Workshop Material

- [Slides](https://docs.google.com/presentation/d/1DRrRZttru7X3vYJjgd_LN1T6w8WhBcrj5ncTRtOEvTE/edit?usp=sharing)

## What is Jest?

Jest is an amazing testing library created by Facebook to help test JavaScript code.

| zero config                                                                 | snapshots                                                                                                               | isolated                                                                               | great api                                                                                                  |
| :-------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------- |
| Jest aims to work out of the box, config free, on most JavaScript projects. | Make tests which keep track of large objects with ease. Snapshots live either alongside your tests, or embedded inline. | Tests are parallelized by running them in their own processes to maximize performance. | From it to expect - Jest has the entire toolkit in one place. Well documented, well maintained, well good. |

## Writing Your First Test

A test is made up of a test name and a callback function that contains our assertions about our code.

Open the `demo.test.js` file inside the `src/__tests__` folder, write the following test and execute in the terminal the following command: `jest -t "1 is 1"`.

Make sure that jest is installed globally by following the steps in the [Getting Started](#getting-started) part of the readme.

```js
test("1 is 1", function () {
  expect(1).toBe(1);
});
```

If everything went fine you should have your first passing test 🎉

```bash
$ jest -t "1 is 1"
PASS  src/__tests__/demo.test.js

Test Suites: 1 skipped, 1 passed, 1 of 2 total
Tests:       1 skipped, 1 passed, 2 total
Snapshots:   0 total
Time:        2.954 s, estimated 6 s
Ran all test suites with tests matching "1 is 1".
```

### `test` and `it`

In order to write a test we use the `test(“”, () => {})` method which takes in a test name and a function (`test()` is also aliased as `it()`). Then, inside the callback function we executing any assertions that we want to make about our code.

```js
test("1 is 1", () => {
  expect(1).toBe(1);
});

// it() is an alias for test()
it("compares 1 to 1", () => {
  // We assert that 1 is 1
  expect(1).toBe(1);
});
```

### Skipping Tests

If you have many tests and you only want to run only some of them, you can use the modifiers that Jest provides.

For this exercise you should open the `modifiers.test.js` file, add the `.only` or `.skip` modifiers after the second test and run in the terminal the following command: `jest modifiers.test.js`

```js
test("1 is 1", () => {
  expect(1).toBe(1);
});

// Only executes this test
test.only("2 is not 1", () => {
  expect(2).not.toBe(1);
});

test("true is true", () => {
  expect(true).toBe(true);
});
```

You should see an output similar to this:

```bash
jest modifiers.test.js
PASS  src/__tests__/modifiers.test.js
 ✓ 2 is not 1 (2 ms)
 ○ skipped 1 is 1
 ○ skipped true is true

Test Suites: 1 passed, 1 total
Tests:       2 skipped, 1 passed, 3 total
Snapshots:   0 total
Time:        1.741 s, estimated 2 s
Ran all test suites matching /modifiers.test.js/i.
```

### Grouping Tests

Sometimes you might have tests that are related or are targeting the same feature of your app. For these cases (and more), you can create a test suite using the Jest `describe` blocks. `describe` blocks can also use the `.skip` or `.only` modifiers.

For this exercise you should execute in the terminal the following command `jest -t "testing numbers"` to execute the first test suite or `jest -t "testing booleans"` to run the second test suite from the `test-suites.test.js` file in the `src/__tests__/` folder.

```js
describe("testing numbers", () => {
  test("1 is 1", () => {
    expect(1).toBe(1);
  });

  test("1 is not 2", () => {
    expect(1).not.toBe(2);
  });
});

describe("testing booleans", () => {
  test("true is true", () => {
    expect(true).toBe(true);
  });
});
```

### Running Tests From The Command Line

We can run tests once we have installed Jest using the command line. If we want to find tests based on the **file name** we can do it this way:

```bash
# if we have a file: `test-file-name.test.js`
# we can use the following command to execute it:
$ jest test-file-name.test.js

# or
$ jest test-file

# if there are several files that start with that
# file name, jest will run all of them
$ jest t
```

If we want to find tests based on the **test name** we can do it this way to run the tests in the `test-suites.test.js` file:

```bash
# this will execute all the tests or describe
# blocks that have a name that contains the name
$ jest -t "testing booleans"

$ jest -t "true is true"
```

### Running Tests From NPM Scripts

We can also execute jest as an npm script in our `package.json` file so that it runs all the tests in our app. Additionally, we can pass the `--watchAll` flag which will execute the tests each time we make a change.

```json
"scripts": {
   "test": "jest --watchAll"
 }
```

## Jest File Naming Conventions

By default, Jest will look for tests in a folder named `__tests__` that contains files named `*.spec.js` or `*.test.js`.

The pattern that Jest uses to find test files by default is:

```js
["**/__tests__/**/*.[jt]s?(x)", "**/?(*.)+(spec|test).[jt]s?(x)"];
```

### Where To Place Test Files?

Tests files should be placed near to the feature we are trying to test inside a `__tests__` folder using the naming conventions explained before.

Tests should be collocated with each feature or part of our app. This way, all the files will be together, both the feature code and the tests.

```bash
src/utils
├── __tests__
│   └── numbers.test.js
└── numbers.js
```

## Matchers

Jest uses _matchers_ to let you test values in different ways.

You can test simple values such as strings, numbers, objects, arrays, or even functions to see how they have been called and with what arguments.

### Basic Matcher Example

A basic example of a matcher usage in Jest is to test if a value is equal to another value by using the `.toBe()` matcher.

```js
test("1 is 1", () => {
  expect(1).toBe(1);
});
```

### 01-exercise

Open the `01-exercise.test.js` file inside the `src/__tests__/` folder and solve the exercise by following the instructions. Then, you can check if your solution is correct by running `jest` from the terminal and passsing in the test suite name: `01-exercise`.

Example: `jest -t "01-exercise"`

For this part you have 10 minutes to solve it. If you get stuck you can find the solution inside the `01-exercise-solution` branch. Once the time has passed the instructor will solve the exercise.

## Author <!-- omit in toc -->

[Dani Lucaci](https://github.com/danilucaci)

## License <!-- omit in toc -->

[MIT](https://choosealicense.com/licenses/mit/)
