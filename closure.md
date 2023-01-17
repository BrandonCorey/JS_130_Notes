### Closure ###
Closures are created when you define a function or method. The closure essentially closes over its environment -- what's in lexical scope.
- So all the things *in scope* of the function are part of the **closure**, along with the variables within its function defintion
- Note: Even if those variaables aren't in lexical scope where the inovcation takes place, the function can still access them

Closure --> function definition + variables in lexical scope of the function
- Does not include variables in scope where the invocation takes place *unless* those variables were also in the definition's scope

The lesson: **where you invoke the function doesn't dictate what it has access to, where you define it does**

Note: A "closure" will store references to all variables referred to within its function definiton
- Launch school tells us to think about this as an envelope object that is attached to the function that stores the references

### Example 1 ###
```javascript
function makeCounter() {
  let counter = 0;

  return function() {
    counter += 1;
    return counter;
  }
}

let incrementCounter = makeCounter();
console.log(incrementCounter()); // 1
console.log(incrementCounter()); // 2
```

### Explanation ###
The closure is the anonymous function that is returned by the makeCounter function.

The makeCounter function defines a variable counter with an initial value of 0, and then it returns a function that can access and update this variable. When this returned function is called, it increments the value of counter by 1 and returns the updated value.

The returned function closes over the variable counter and stores its reference, so even after the makeCounter function has finished executing and its local scope is no longer available, the returned function still has access to the counter variable and can update its value.

When incrementCounter is called the first time, it increments the value of counter to 1 and returns it, the second time it increments it to 2 and returns it and so on.

### Example 2 ###
```javascript
function add(first, second) {
  return first + second;
}

function makeAdder(firstNumber) {
  return function(secondNumber) {
    return add(firstNumber, secondNumber);
  };
}

let addFive = makeAdder(5);
let addTen = makeAdder(10);

console.log(addFive(3));  // 8
console.log(addFive(55)); // 60
console.log(addTen(3));   // 13
console.log(addTen(55));  // 65
```
### Explanation ###
The closures are the anonymous functions returned by the makeAdder function.

makeAdder takes a single argument firstNumber and returns a new function that takes a single argument secondNumber and returns the result of calling add(firstNumber, secondNumber). The returned function closes over the firstNumber variable and add function, so it has access to these values and can use them to compute the result.

When addFive is called with the argument 3, it uses the closed-over value 5 as the first argument and 3 as the second argument to call the add function which returns the sum 8. Similarly, when addTen is called with the argument 3, it uses the closed-over value 10 as the first argument and 3 as the second argument to call the add function which returns the sum 13.
