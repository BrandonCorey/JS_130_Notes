## Testing SEAT Approach ##
1. Set up the necessary objects.
  - Use `beforeEach`
2. Execute the code against the object we're testing.
  - Run the code snipped that we are going to test
3. Assert the results of execution.
  - Use `expect` and the methods of the returned object to assert the expected value
4. Tear down and clean up any lingering artifacts.
  - Use `afterEach`

### Previously, we did step 2 and 3, lets tackle step 1 ###

To create a new object (or any other variable) to be tested for each test, we can use the `beforeEach` function
- This function takes a callback as an argument to execute before each test runs
- `beforeEach` does **NOT ** run inside of the test body, it re-executes every time a new `test` is seen
- As a result, we must declared variables outside of `beforeEach` so we don't try to redeclare the same variable over and over when it runs
  - Reassigning the same variable is fine, as we know
  - This also lets us keep our variables in a place that is lexically in scope for all of our test cases

**NOTE**
- There is also an `afterEach` function that can be used for teardown, but we don't need that here
  - This function will execute the callback passed to it _after_ each test
- Teardown may include logging things to console, clean up files, disconnect from database etc

```javascript
const Car = require('./car');

describe("car Instance Tests", () => {
  let car; // in scope for all subsequent tests
  beforeEach(() => {
    car = new Car(); // Before each test is ran, a brand new car is created and reassigned back to our car variable
  });

  test("has four wheels", () => {
    expect(car.wheels).toBe(4);
  });

  test("mileage is null", () => {
    expect(car.mileageInfo).toBeNull();
  });

  test("instances are identical", () => {
    let newCar = new Car();
    expect(newCar).toEqual(car);
  });

  test("car cannot be driven", () => {
    expect(car.drive).toThrow();
  });

  test("wheels is truthy value", () => {
    expect(car.wheels).toBeTruthy();
  });

  test("car  has a 'wheels' property", () => {
    expect(car.wheels).not.toBeUndefined();
  });

  test("car is in car array", () => {
    let arr = [];
    arr.push(car);

    expect(arr).toContain(car);
  });

  test("string contains car", () => {
    let str = 'I am very scared';
    expect(str).toContain('car');
  });
}); 
```
