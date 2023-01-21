## Exceptions ##
Errors messages that are thrown when JavaScript cannot recover from an error
- Program will be automatically terminated
- "throw" and "raise" can be used interchangeably
- "error" message however, does not always mean exception
  - Could be something as simple as a `console.log`


## Throwing excpetions ##
- Most we've seen so far are raised internally (i.e ReferenceError, SyntaxError, TypeError);
- They can also be defined manually
- All exceptions are objects, either the `Error` object or instances of the `Error` object (like the ones mentioned above)

```javascript
fuction div(first, second) {
  if (second === 0) throw new Error ('Cannot divide by zero');
  return first / second;
}
```
```javascript
const DivideByZeroError = class extends Error {}

function div(first, second) {
  if (second === 0) {
    throw new DivideByZeroError('Cannot divide by zero');
  }
  return first / second;
}
```

## Catching exceptions ##
We can use the `try` and `catch` statements to resolve excpetions that are raised
- This is a good use case of explicitly created a new error class like above
- You generally want to know exactly the type of error that may be raised
- When an exception is thrown, it will always look for `try` blocks that contain the code that caused it before terminating
  - If it finds one, the code in the catch block will be executed

```javascript
function divideOneBy(divisor) {
  try {
    return div(1, divisor);
  } catch (error) {
    if (error instanceof DivideByZeroError) {
      console.log('Division by 0 ignored');
    } else {
      throw error; // If we can't determine what the expcetion is, throw it, don't try to handle it
    }
  }
}
```

### Exceptions should be used for exceptional behavior ###
- Do not throw exceptions for flow control type issues
  - The divide by 0 is an exmaple of when it might not be needed
  - Any type of input validation that can be controlled probably should not raise an exception

- Throw them when there is behavior that should not be ignored or is truly anomolus
  - ex) trying to load a file that may fail
  - Only way to detect this is by trying and seeing if it works

- Only handle exceptions you believe can be recovered from successfully
  - Only handle if you're confident the handler will not throw another expceiton itself
  - handler should do as little as possible (ignore exception, return error value, log a message, throw another exception)
