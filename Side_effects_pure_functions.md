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

NOTE: Functions producing unexpected side effects are a major source of bugs

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
