## Asynchronous JS ##
Code can be run asynchronously in JS. Meaning when the runtime encounters the code, it does not execute it fully until a later point (milliseconds, seconds, days, hours)

### `setTimeout` ###
- `setTimeout` is one of the easiest ways to run code asynchronously
- Note that the invocation of `setTimeout` is not delayed, only the exeuction of the callback function passed to it

```javascript
setTimeout(function() { // 1
  console.log('!'); // 5
}, 3000);

setTimeout(function() { // 2
  console.log('World'); // 4
}, 1000);

console.log('Hello'); // 3
```

- Its important to note that above, between steps 3 and 4, and 4 and 5, JS does **nothing** for a gap of 1000ms, then 3000ms. Its just waiting to run the code

### Callback passed to `setTimeout` only runs when JS is not doing anything else ###
- Will always run code without a timeout delay before code that has one (even if the delay is 00
- Code that has the same delay will execute top to bottom like normal
```javascript
// Be sure you run this code from a file!

setTimeout(function() { // 1
  console.log('!'); // 4
}, 0);

setTimeout(function() { // 2
  console.log('World'); // 5
}, 0);

console.log('Hello');  // 3
```

### More Notes ###
Lets look at the following two examples
- The first example logs the correct values after 1 second
- The second example logs `11` every time
```javascript
const delayLog = () => {
  for (let sec = 1; sec <= 10; sec++) {
    setTimeout(() => console.log(sec), sec * 1000);
  }
}
```
```javascript
const delayLog = () => {
for (var sec = 1; sec <= 10; sec++) {
    setTimeout(() => console.log(sec), sec * 1000);
  }
}
```

### Explanation ###
**In both examples**
- The for loop finishes exeuction before a single function is executed by `setTimeout`
- A closure is formed with `sec` and the callback definition within `setTimeout`

**Differences**
NOTE: (JS handles counters with closure in a special way, but treats them similar to newly scoped variables on each iteration)
- In the first example, we use `let` to declare variables. These are block scoped. With closure, JS *treats* this as if, on each itertion, a new `sec` variable is declared
  - A new variable means a new `sec` variable is closed over on each iteration by the callback passed to `setTimeout`
  - This means a new closure is formed (as the enviroment is changed on each iteration)
  - When each callback is executed, the value of counter variable for their respective closure is used, which will reflect the state of the counter when the closure   was formed
  - This will log the correct incremental values after the delay (1 - 10)
- In the second example, we use `var` to declare variables. These are function scoped, and only assigned/reassigned in the loop, not declared
  - As a result, only a single closure is formed with the callback function as the environment around it never changes. `sec` is reassigned, but its the same variable
  - Because of this, after the loop finishes executing, the closure for the callback has a reference to the fully incremented `sec` variable
  - Because of this, the calback logs `11` each time, which is the final value of the counter after the for loop (since it stops incrementing when its greater than 10)

### More notes on the above ###
The following code produces the same effect as using `var` to declare `sec
```javascript
const delayLog = () => {
  let sec;
  for (sec = 1; sec <= 10; sec++) {
    setTimeout(() => console.log(sec), sec * 1000);
  }
}
```

This is more similar to what JS does behind the scenes what when using closure with a for loop using let
```javascript
const delayLog = () => {
  let sec;
for (sec = 1; sec <= 10; sec++) {
    ((delay) => (setTimeout(() => console.log(delay), delay * 1000)))(sec);
  }
}
```
- Here, instead of the `setTimeout` callback closing over `sec`, it closes over `delay` in the definition of the IIFE
- In reality, a new `sec` is **not** declared on each iteration, as incrementing would be impossible, but JS does magic behind the scenes so that closure treats it like a new counter is created for the purpose of closure having access to these intermediate values

### `setInterval` and `clearInterval` ###
Works similar to `setTimoeout`, but instead allows you to execute a callback at certain intervals instead of after a delay
- Can use `clearInterval` to stop the `setIntervals` execution of the callback passed to it
- `setInterval` returns an `intervalID` that can be used to cancel its execution using `clearInterval
- `setIntveral` also bases its delays on milliseconds
```javascript
const stayingAlive = () => {
  setInterval(() => console.log('staying alive'), 1000);
}

stayingAlive();
// stayin alive
// stayin alive
// stayin alive
// ...
```
```javascript
const stayingAlive = () => {
  return setInterval(() => console.log('staying alive'), 1000);
}

let stayingAliveID = stayingAlive();

const notAlive = (intervalID) => clearInterval(intervalID)
notAlive(stayingAliveID);

// Nothing is logged since we cancelled it
```
