## Unit Testing ##
This is what we are using jest for currently

### Vocab ###
- Test Suite - A set of tests that accompanies a program or applicaiton
- Test - A specific situation or context being tested. May sometimes be referred to as a **spec**
- Assertion - Verification that confirms your program did what it was supposed to. Ex) Did a function return the correct value (Also called **expectation**)

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
  });
});
```
**Skipping tests**

Any test in a file can be skipped by using either `test.skip` or `xtest` where `test` would normally go
- This is good if you have a test writtent that you don't want to run yet, or if the test is broken

### Matcher Methods ###
The most common matcher methods. The total list is much longer
- `toBe` - Fails unless actual value === expected value
- `toEqual` - Same as to be but also tests for object value equality ie. `[1, 2, 3]` is equal to `[1, 2, 3]`
- `toBeUnefined` - Fails unless actual value is `undefined`. Same as `toBe(undefined)`
- `toThrow` - Fails unless expression passed to `expect` raises an exception
- `toBeNull` - Fails unless the actual value is `null`
- `toBeTruthy` - Fails unless the actual value is truthy
- `toContain` - Fails unless the given array contains a certain value. Can also be used on strings to check for contained substrings

```javascript
const Car = require('./car');

describe("Car Instance Tests", () => {
  test("Has four wheels", () => {
    let car = new Car();
    expect(car.wheels).toBe(4);
  });

  test("Mileage is null", () => {
    let car = new Car();
    expect(car.mileageInfo).toBeNull();
  });

  test("Instances are identical", () => {
    let car = new Car();
    let newCar = new Car();
    expect(newCar).toEqual(car);
  })

  test("Car cannot be driven", () => {
    let car = new Car();
    expect(car.drive).toThrow();
  })

  test("Car has wheels", () => {
    let car = new Car();
    expect(car.wheels).toBeTruthy();
  })
}); 
```
