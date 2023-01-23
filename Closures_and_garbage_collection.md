## Garbage collection for Closure ##
So I've learned that references and primitives are generally stored on the stack, while objects are stored on the heap

If thats the case, then why is closure possible, shouldn't the variables that are defined within a function and referenced by inner functions be tossed away after the outer
function returns?

Normally, any variables defined in the function would be deallocated after execution, but this is not what happens when a closure if formed

### A closure is A REAL OBJECT ###
- It is a special object in JS, it cannot be accessed, but it is there, and it stores references to all in-scope variables
- Closures are *function scoped*, but because Node wraps all code in a wrapper function, globally scoped variables form a closure with all functions
- Because a closure is **AN ACTUAL OBJECT**, it is stored on **THE HEAP**
- As such, all of the references the closure contains are also stored on the heap (and subject to GC)
- the variable references stored in the closure give us a way to access these variables going forward
- This means that the variables, which are still on the stack, may live on if we reference them in other parts of our program

```javascript
let incrementCounter = (function() {
  let counter = 0; // closed over by inner function, reference to counter variable is stored INSIDE closure object
  return () => {
    counter += 1; // Returned function increments our value stored in counter variable, which is located in closure on heap
    return counter;
  }
})();

incrementCounter(); // Looks for counter in local scope, can't find it, then looks in closure, finds it, incremenets it
incrementCounter(); // same as above
```

### Lookup Sequence ###
Where do variables referenced in a functions closure fit into the lookup sequence?

When a function is executed, it checks for the value of a variable in the following order:
1. Local scope: The function first checks if the variable is defined within its own local scope. If it is, the function uses the value stored in the local scope.
2. Closure scope: If the variable is not found in the local scope, the function then checks the closure object associated with it, if it has one. 
3. If the variable is not found in any of the above scopes, the function will throw a ReferenceError (unless it was declared with `var`, then it is undefined)
