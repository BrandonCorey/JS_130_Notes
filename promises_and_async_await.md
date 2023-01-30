## Promises ##
Promises give us a way to use asynchronous code in JS
- Promises are are objects of the `Promise` constructor
- Each promise takes a single argument, a callback that contains two (one optonal) arguments
  - The parameters for the callback are two more callbacks, a `resolve` callback, and a `reject` callback
  - These will be invoked conditionally based on how the promise settles
- The **Fulfillment value** of a promise is the argument passed to either the `resolve` or `reject` callback, depnding on how the promise settles


### Promise vocab ###
- Pending: A promise that has not been settled
- Setted: A promise that has either resolved or rejected
- Resolve: A promise that has returned the `resolve` callback
- Rejected: A promise that has returned the `reject` callback
- Fulfilled: A promise that has a fulfillment value
- Fulfillment value: The value passed to the `resolve` or `reject` callback
  - Note: Fulfilment is based on the fulfilment value, not whether or not the callback has been executed yet

### `Promise.prototype` methods ###
- `then` - allows you to pass resolve and reject callbacks to a pending promise. Returns a new promise. Can be used to chain
- `catch`- allows you to supply a reject callback for multiple chained promises, instead of having to supply one to each individually
- `finally` - allows you to supply a callback for after a promise has been settled. 


### `Promise` methods 
- `all` - Accepts an array of promises, and returns a single promise. Only resolves if all promises resolve. Returns an array of resolved values
  - If a promise in the array argument rejects, returns rejected promise
- `race` - Accepts an array of promises, returns a single promise. Returns first promise to settle, either resolve or fail
- `allSettle`- Accepts an array of promises. Returns a promise that settles when all input promises settle

## `async` and `await` ##
Allow us to write asynchronous functions easier, syntactic sugar to promise instance methods
- Can put `asnyc` in front of any function declaration (or expression)
- Can use `await` to wait on a promise to settle
  - Settled promise returns the fulfillment value of the promise

### Important Note ###
- Remeber that `await` used with a promise will return a fulfillment value (argument to resolve/reject), whereas `then` returns a new promise
- `async` and `await` are newer syntax, and are more popular then using `then` since it allows you to write synchronous looking code
- `then` lets us immediately provide callbacks to do something with the fulfilment value, whereas `async` and `await` let us use it like a normal variable

```javascript
// Create promise

const createRequest = (website) => {
  return new Promise((resolve, reject) => {
    if (website === 'google') {
      let count = 3;
      let countID = setInterval(() => {
        console.log(count);
        count -= 1;

        if (count === 0) clearInterval(countID);
      }, 1000);

      setTimeout(() => {
        resolve('Connection successful!');
      }, 4000)
    } else {
      reject('Can only make requests to google');
    }
  });
}

const printMessage = (message) => console.log(message);

// With promise `then` syntax
const sendWithPromiseMethods = (website) => {
  createRequest(website).then(printMessage, printMessage) // Invokes asynchronous function, then invokes correct callback based on how promise settles
}


// With async and await

const sendWithAsyncAwait = async (website) => { // telling JS our function is asynchronous
  try {
    const response = await createRequest(website); // We await createRequest to settle. If it resolves, it saves "Connection Successful!" to response. This is a STRING
    printMessage(response);
  } catch (error) { // Catch block will pass our reject agument to "error" so error in this case is "Can only make requests to google"
    printMessage(error);
  }
}


//sendWithAsyncAwait('facebook');
//sendWithPromiseMethods('google');
```
