## Immediately Invoked Function Expressions ##
These are functions expressions that are defined, evaluated, and invoked all at once
- This can be done by surrounding the expression in parenthesis, then calling it (using another set of parenthesis, like a normal function call);
  - Can use this for any type of function syntax (including arrow)
- The parenthesis tell JS to evaluate the function definition as an expression. We then use parenthesis to pass any args to the function for evlauation.
  - NOTE: You don't need to wrap the IIFE in parenthesis if you're storing its evaluation value in a variable, but SHOULD still use them as good practice
```javascript
(function(name) {
  console.log(`My name is ${name}`);
})('Brandon'); // 'My name is Brandon'

(function() {
  console.log('Hello world');
})(); // 'Hello world'

((first, second) => first + second)(5, 3); // 8
```

## Benefits ##
## Allows you to create private scope amidst a larger program ##
- This means you do not have to worry about clashing variable names, including function name
- The example below shows how nothing leaks outside of the private scope of the IIFE
```javascript
// 1000 lines of JS above

// Remove duplicates in an array
console.log((function(array) {
  return array.reduce((arr, value) => {
    if (!arr.includes(value)) arr.push(value);
    return arr;
  }, []);
})([1, 1, 5, 5, 3, 4, 4, 5]));

// 1000 lines of JS below
```
**Note: In ES6 and later, you can accomplist the same using blocks**

```javascript
// Example of using blocks for private scope
{
  let array = [1, 1, 5, 5, 3, 4, 4, 5];
  let deDuped;

  deDuped = array.reduce((arr, value) => {
    if (!arr.includes(value)) arr.push(value);
    return arr;
  }, []);

  console.log(deDuped);
}
```
## Can be used with closure to create Private Data ##
- We can use this pattern to eliminate the need to define a function that creates our return function
  - This creates one less uneeded function name, and one less function invocation.
- Notice below how we don't need a factory function to create a counter
  - We can use the IIFE as the factory, then invoke it immediately to return the useful function
```javascript
const counter = (function() {
  let counter = 0;
  return function() {
    counter += 1;
    return counter;
  };
})();

counter();
counter();
counter();
```
