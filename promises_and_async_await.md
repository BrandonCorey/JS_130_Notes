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
  createRequest(website).then(printMessage, printMessage)
}


// With async and await

const sendWithAsyncAwait = async (website) => {
  try {
    const response = await createRequest(website); // response will save the argument passed to either 'resolve' or 'reject' based on the result of the request
    printMessage(response); // In this case, response is 'Connection Successful', so we are printing that
  } catch (error) {
    printMessage(error);
  }
}


//sendWithAsyncAwait('facebook');
//sendWithPromiseMethods('google');
```
