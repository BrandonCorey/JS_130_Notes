## Strict Mode ##
Optional mode that modifies the semantics of JavaScript and prevents certain errors and syntax

To enable, add this text to beginning of program file or function definition
```javascript
"use strict";
```

### What does it do? ###
- Throws certain errors that fail silently in sloppy mode
- Prohibits some code that inhibits JS ability to opmitize a program
- Prohibits using names or syntax that may conflict with future versions of JS

### Why do we use it? ###
- To prevent or mitigate bugs
- To help make debugging easier
- To help code run faster
- To help avoid conflicts with future changes to the language

### When to use it? ###
Use it in any new code you write
- If using on old code, its safe it use it at the function level
- Don't use it at the global level for old code that it may break

### Notes about strict mode ###
- Strict mode is lexically scoped
- Enabling strict mode for a function does so for the entire definition, including nested functions
- **Cannot enable** strict mode for a **block**, must be a function definition
- Strict mode cannot be disabled within its scope after it has been enabled
- **ES6 classes** automatically enable strict mode
- Implicitly scoped global variables are not allowed (must use `let`, `const`, or `var`, not declaring a variable will throw a reference error)
  - Helps stop the creation of unwanted global variables
- Implcit execution context is set to the `undefined`, not the `global` object
  - Helps spot context loss sooner
- Cannot use numbers with leading 0's (JS uses an octal base for the number when this is done)

**Other notes**
- Cannot use two parameters with same name
- Can't use certain keywords as variable names
- Cannot use delete operator on a variable name
- disables `with` statement`
- Limits `argument` object accessibility

```javascript
// Example of function scoped strict mode
function foo() {
  "use strict"
  console.log('foo'); // runs in strict mode
}

function bar() {
  foo(); // invocation runs in sloppy mode, but 'foo' runs in strict mode
}
```
```javascript
// Example of undeclared variables throwing errors
function test() {
  foo = 'hello';
}

test();
console.log(foo); // 'hello';
console.log(global.foo); // 'hello';

function newTest() {
  "use strict"
  bar = 'world'; // ReferenceErorr: bar is not defined
}

newTest();
```
```javascript
// Example of implicit context of the program using strict mode
"use strict"
const obj = {
  name: 'Brandon';
  changeName(name) {
    this.name = name;
  }
}

const changeName = obj.changeName;
changeName('Nug'); // TypeError: Cannot set property 'name' of undefined (implicit context of program is undefined, not global object)
```
