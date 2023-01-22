### Side effects ##
A function that does any of the following is said to have side effetcs
- Reassigns a non local variable
- Mutates an object refernced by a non local variable
- reads or write to any data entity (files, netowrks connections, database) that are non local to your program
- Raises an exception
- Calls another function that has side effects

NOTE: Its more accurate to speak about function *calls* having side effects, not definitons
- This is because a function may only have side effects when invoked in a specific way
- HOWEVER: When a function will *always* produce side effects, we can say the *function* itself has side effects

```javascript
[1, 2, 3].map(num => console.log(num)); // invocation of function (map) has side effects

const timesTwo = arr.map(num => console.log(num * 2)); // function (timesTwo) has side effects
```
