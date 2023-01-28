## Asynchronous JS ##
Code can be run asynchronously in JS. Meaning when the runtime encounters the code, it does not execute it fully until a later point (milliseconds, seconds, days, hours)
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
