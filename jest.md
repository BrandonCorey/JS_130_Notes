## Unit Testing ##
This is what we are using jest for currently

### Vocab ###
Test Suite - A set of tests that accompanies a program or applicaiton
Test - A specific situation or context being tested. May sometimes be referred to as a **spec**
Assertion - Verification that confirms your program did what it was supposed to. Ex) Did a function return the correct value (Also called **expectation**)

### Jest Specifics ###
`describe` 
- Function that accepts a string description and a callback `test` function
  - This method is not required for tests, but is typically used to group a set of tests together within your test file
`test`
- Function that also accepts a string description and a callback function
  - The callback function makes an **assertion** that will be tested

**Assertions**
Each assertion in jest begins with the invocation of the `expect` function
- These function is passed a value we want to assert (test) called an *actual value*
- `expect` returns an object with a variety of **matcher methods** that compare our *actual* value with our *expected* value
  - One example of a matcher method is `toBe`

```javascript
const Car = require('./car');

describe("Car class", () => {
  test("Has four wheels", () => {
    let car = new Car();
    expect(car.wheels).toBe(4);
  })
})
```
