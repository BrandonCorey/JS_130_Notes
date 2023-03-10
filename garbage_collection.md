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

**Heap**
- Everything else lives here
- All objects plus strings and bigints will be here
  - Unlike with most primitives, JS cannot determine the amount of memory needed during creation for objects, strings, bigints. A number is always 64 bit, an object is variable. The amount of memory is not known until the definition of the object is encountered during execution
- Memory is allocated as values are created during execution
- Since references are on the stack, and objects on the heap, objects won't be GCed until all of their references in the program are gone
  - Scope has nothing to do with GC, its about whether or not things are still refernced through the rest of the program

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

// Meanwhile, that 5 was de-allocated from the stack as soon as the function finished executing
// Even if we returned it, the VALUE would be returned, not a reference.
//  HOWEVER if we closed over x, the closure object would store a reference to the variable on the heap, and x would only be deallocated after it is no longer     referenced
// Since that specific 5 in memory is going to be gone after the exeuction no matter what, the memory can be given back
```
