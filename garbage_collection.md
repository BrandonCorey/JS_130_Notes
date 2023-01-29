## Garbage Collection ##
An algorithm implemented in JS that deallocates memory being used to store data in the heap
- JS handles memory allocation and garbage collection behind the scenes

### Stack vs heap ###
**Stack**
- Most primitives with fixed sizes (so not strings or bigints) are stored on the stack
- References also live on the stack (NOT THE OBJECTS THEY REFERENCE HOWEVER)
  - Since most primitives and references live on the stack, most variables themselves live on the stack
- The stack does not participate in garbage collection
- Because they have fixed sizes (things like `number`, `null`, `undefined`), JS can determine how much memeory to allocate at the start of the function/block during creation
- When the block / function is done executing, the memory can be deallocated
  - This makes sense, primitives cannot be refernced when they are out of scope like objects can

**Heap**
- Everything else lives here
- All objects plus strings and bigints will be here (these all have dynamic sizes and cannot be allocated ahead of time)
- Memory is allocated as values are created during execution
- Since references are on the stack, and objects on the heap, objects won't be GCed until all of their references in the program are gone
  - Unlike the stack, memory is not deallocated when variables go out of scope
  - This is why we can do things like closure, or access an object out of scope, or call a function / method out of scope through their references

```javascript
function test() {
  let x = 5;
  const anon = function () {
    console.log('hello world');
  }
  return [anon, anon];
}

let [outOfScope, outOfScope1] = test();
outOfScope === outOfScope1; // true

// We have two references to an out of scope function (object)
outOfScope = 1; // Now we only have one reference left
outOfScope1 = 0; // That was the last one, the function that was being reference will now be garbage collected

// Meanwhile, that 5 was unallocated from the stack as soon as the function finished executing
// Even if we returned it, the VALUE would be returned, not a reference. 
// Since that specific 5 in memory is going to be gone after the exeuction no matter what, the memory can be given back
```
