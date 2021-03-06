# intro-to-unit-testing

The following instructions **ARE NOT** to install/use this repo; they are to recreate for scratch this project.

### Setting up the repo

```sh
npm init -y
git init
touch .gitignore
echo -e "# dependencies\nnode_modules/\n" >> .gitignore
echo -e "# coverage\ncoverage/\n" >> .gitignore
```

### Installing dependencies

From the terminal, install the `jest` package
```sh
npm install --save-dev jest
```

Once installed, let's configure the `package.json` to use that when calling `npm test`
```json
  "scripts": {
    "test": "jest"
  }
```

### Test preparation

For each JS file that needs to be tested
* Make sure to export each functions from the file with `module.exports`
* Create a brand new file called `file.test.js`
* In the new file, import (with the `require` keyword) each function to be tested

### Writing Tests

1. Invoke the `test()` function
2. Pass two arguments:
   * A string that describes the test
   * A callback functions that runs the test (see point 3 below)
3. Declare the actual and the expectation values
4. Invoke `expect()` with the actual parameter
5. On `expect()` chain up any **matcher methods** such as **toBe** or **toThrow** with the expectation parameter. For more examples, refer to [Common Matchers](###common-matchers)

**Real example**

```js
test("Sum 1 and 2", () => {
    const actual = sum(1, 2);
    const expectation = 3;
    expect(actual).toBe(expectation);
})
```

### Common Matchers

Matchers are methods that can be "chained" after `expect()`.
The simplest way to test a value is with exact equality.

* toBe()
* not.toBe()
* toEqual()
***toEqual** works on objects and recursively checks every field of an object or array*

#### Truthiness

* toBeTruthy()
* toBeFalsy()

#### Numbers

* toBeGreaterThan()
* toBeGreaterThanOrEqual()
* toBeLessThan()
* toBeLessThanOrEqual()
* toBe()
* toEqual()
***toBe** and **toEqual** are equivalent (for numbers)*

#### Strings

* not.toMatch(/regex/)
* toMatch(/regex/)

#### Arrays and iterables

* toContain()

#### Exceptions

* toThrow()
* toThrow(Error)
* toThrow('insert here the exact error message');
* toThrow(/regex/);

#### And More

For a complete list of matchers, check out the [reference docs](https://jestjs.io/docs/en/expect)

### Test suite

A test suite, less commonly known as a 'validation suite', is a collection of test cases.
With Jest, we can group together many `test()` functions into one bigger suite.
This is done by wrapping everything in `describe()`.

```js
describe("Properly adding two numbers", () => {

    test("Sum 1 and 2", () => {
        const actual = sum(1, 2);
        const expectation = 3;
        expect(actual).toBe(expectation);
    })
    
    test("Sum 2 and 3", () => {
        const actual = sum(2, 3);
        const expectation = 5;
        expect(actual).toBe(expectation);
    })

})
```

### Test Coverage

Testing specific functionality is cool, but not enough; we want to make sure that the whole content of our files is properly tested. Or at least most of it.
This is when the concept of **coverage** comes in.

1. Modify package.json
2. Pass the new `--coverage` option flag to jest
3. Re-run the tests

![Terminal Coverage Report](./images/terminal-coverage-report.png)

With the Jest default configuration, the same coverage report is also generated in a `lcov` format under `./coverage` folder

![HTML Coverage Report](./images/html-coverage-report.png)