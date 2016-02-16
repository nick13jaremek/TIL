# The problem

Having a set of Mocha tests that use the `mockery` library to create mocks for a tested-file's dependencies.

Having a `describe` block with two `it` test cases, where each test case defined its own `mockery` mocks, the second test case was using the mocks defined in the first one.

# Example

````

// file.js

const dependencyFunction = require('./dependency');

dependencyFunction()
  .then(() => console.log('Resolved'))
  .catch((error) => console.log('Rejected', error);


//=============================================================================

// file_test.js
describe('Test block', () => {

  it('first test case', done => {
    mockery.registerMock('./dependency', () => Promise.resolve());
    // A call to the 'dependency' function will return a Promise resolve callback
  });

  it('second test case', done => {
    mockery.registerMock('./dependency', () => Promise.reject());
    // A call to the 'dependency' function  will return a Promise resolved callback even though the mock in this test case should return a Promise rejected callback
  });
});
````

In this `describe` block, both test cases would return a Promise resolve() callback when calling the function on the `./dependency` file.

# The solution

Deregister and cleanup the mocks after each test case by using an `afterEach` Mocha block inside the `describe` block, as follows:

````
afterEach(() => {
  mockery.deregisterAll();
  mockery.disable();
});
````

This block will ensure each test case starts with its own defined `mockery` mocks.

