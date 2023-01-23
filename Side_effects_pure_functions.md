### Side effects ##
A function that does any of the following is said to have side effetcs
- Reassigns a non local variable
- Mutates an object refernced by a non local variable
- reads or write to any data entity (files, netowrks connections, database) that are non local to your program
- Raises an exception
- Calls another function that has side effects

NOTE: Its more accurate to speak about function *calls* having side effects, not definitons
- This is because a function may only have side effects when invoked in a specific way
- HOWEVER: When a function produces side effects when used as intented, we say the *function* itself has side effects
  - Used as intended:
    - Expcted number of args is passed
    - Expcted data type is passed
    - Function is called at expected point in the program 

NOTE: If a function has side effects *only* on local variables, it is still considered to NOT have side effects

```javascript
[1, 2, 3].map(num => console.log(num)); // invocation of function (map) has side effects

const timesTwo = arr => arr.map(num => console.log(num * 2)); // function (timesTwo) has side effects
```

### Side effects through reassingment ###
This is a function that reassigns any variable that is not declared within its definition
```javascript
let num = 0;

const incrementNumber = () => num += 1; // reassigns num to a new number on each invocation
incrementNumber();
console.log(num); // 1
```

### Side effects through mutation ###
This is a function that mutates an object that is referenced by a variable that is not declared within the functions definition

```javascript
let array = [1, 2, 3]
const descOrder = (arr) => arr.sort((b, a) => a - b);
descOrder(array);
console.log(arr); // [3, 2 1]
```

**NOTE:**
When a new array tranformed array is returned from a function, this is side effects through reassignemnt NOT mutation
```javascript
const twoTimes = (arr) => arr.map(num => num * 2);
array = twoTimes(arr);
console.log(array); // [6, 4, 2]
```

### Side effects through input output (I/O)
Common IO side effects can be seen below

- Reading from a file on the system's disk
- Writing to a file on the system's disk
- Reading input from the keyboard
- Writing to the console
- Accessing a database
- Updating the display on a web page
- Reading data from a form on a web page
- Sending data to a remote web site
- Receiving data from a remote web site
- Accessing system hardware such as:
  - The mouse, trackpad, or other pointing devices
  - The clock
  - The random number generator
  - The audio speakers
  - The camera

```javascript
const readline = require('readline-sync');
let answer = readline.question('How old are you'); // This method "question" produces side effects
```
```javascript
let date = new Date(); // side effects, accesses system clock
let rand = Math.random(); // side effects, accesses random number generator
```

### Side effects through exceptions ###
If a program raises an excpeiton
- And doesn't handle it, it has side effects
- If it handles it, and the catch block  has side effects, it has side effects
- If it handles it, and the catch block does NOT have side effects, it does not have side effects

```javascript
function multiply(num1, num2) {
  try {
    if (num1 === undefined || num2 === undefined) {
      throw new Error('Error: Cannot multiple by undefined'); // side effects if this is executed and not caught successfully
    }
  } catch (error) {
      console.log(error.message); // side effects if this is executed (because of log)
      return NaN;
  }
  return num1 * num2; // No side effects we reach this, just returning a number
}
```
### Mixing side effects and return values ###
Generally, we should try to avoid mixing side effects and *useful* return values
- A useful return value is a value that we intend to do something with, not an arbitrary value or value that is always the same
- This rule can, and **must** be broken in certain situations. Below are some common examples:
  - Reading input from the user, then returning the value
  - Reading input from a database,then returning the value
  - Logging a value to the console before returning it

### Pure Functions ###
These are functions that:
- Have no side effects
- Will always return the same value if passed the same arguments
  - This is the most important part of pure functions
  - Means nothing else in the program, aside from the arguments being passed in, can influence the function during its lifetime
    - A functions lifetime can vary:
    - A globally scoped function will exist until the garbage collector scoops it up
    - A nested function, or anything within the definition that is not part of a closure, is destroyed after a single invocation
      - On new invocations, these values will be reallocated to a new slot of memory, but the original is destroyed after execution
  - Also means that pure functions have no effect on any other parts of the program
  - Similar to side effects, we can refer to either functions themselves or their invcoations as **pure** or **impure**

```javascript
const deDupe = array => {
  return array.filter((el, idx) => {
    return idx === array.indexOf(el);
  });
}

deDupe([1, 1, 2, 2, 3, 3]); // [1, 2, 3];
// This is pure. It produces no side effects, and will always return [1, 2, 3] when [1, 1, 2, 2, 3, 3] is passed in
```
