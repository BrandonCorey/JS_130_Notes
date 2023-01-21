## Modules ##
Modules are just pieces of code that can be exported to a file

### Problems modules try to address ###
Large programs that are a nightmare to traverse and keep track of

### Benefits ###
- Each module can work on a seperate problem (seperation of conerns)
- The means that each module's code will not become tangled with each other
- Makes it easier to work with private data 
  - (since each module will have its own private environment, things must be explicitly exported to be made public)
- Its easier to import a module then copy/cut and paste code from another file

### CommonJS modules ###
- Native to the language
- Uses `require` syntax to import a module
  - NPM modules usuall just require the name of the module as the argument
  - User created modules require the filepath (in relation to the current directory)
- Uses `module.exports` to export a module
- Only works in Node, too slow for the browser (loads synchronously, not asynchronously)

**Important variables**
`module` - An object that represents the current module
`exports`- Name(s) exported by module (same object is referenced by `module.exports`)
`require` - function that loads module
`__dirname` - absolute pathanme of the directory that contains the module
`__filename` - absolute pathname of the file that contains the module

```javascript
// File sum.js
const sum = array => array.reduce((a, b) => {
  return a + b;
});

moudle.exports = sum;

// New file in same directory
const sum = require('./sum');

console.log(sum([1, 2, 3, 4, 5])); // 15
```
