### Closusre ###
Awesome explanatin below, from launch school

**A closure lets a function access its definition envrioment, regardless of when and where the program invokes the function**

### Private Data ###
- Because closures can reference variables that are no longer in scope, we can use them to access _private data_ within the function definition itself
- We can use factory functions to return other functions or objects that use closure to access private data
  - This allows us to enforce access to the private data via whatever way we decide
  - Restricting access forces other developers to use our interface (which is good for data integrity)
  - We can use an object to supply an API that provides methods to interract with the private data
  - This allows the API to stay the same, regardless to changes in implementations of the object

### Example ###
- `list` is private data
- It cannot be accessed without from outside the function without using our API
- Each of our methods forms a closure with `list` (reference to list VARIABLE is passed to "envelope" attached to method)
  - This points us to the variable, which points us to a reference, which points us to the array
  - This allows us to access the array after the `makeList` invocation has finished executing, as we have the memory location of its local variable

```javascript
const makeList = () => {
  const list = [];
  
  return {
    add(item) {
      let itemIdx = list.indexOf(item);
      if (itemIdx === -1) {
        list.push(item);
        console.log(`${item} added!`);
      }
    },

    remove(item) {
      let itemIdx = list.indexOf(item);
      if (itemIdx !== -1) {
        list.splice(itemIdx, 1);
        console.log(`${item} removed!`)
      }
    },

    list() {
      if (!list.length) console.log('The list is empty.');
      else list.forEach(item => console.log(item) + '\n');
    }
  }
}
```
