## JS Engine Phases ##

### Creation ###
- Takes note of all declarations in program
  - Also takes not of their scope

### Execution ###
- Runs programs line by line
- Does hoisting for all declarations (moves them to top of scope)
  - variables declared with `let`, `const` and `class` are not accessible before initalization, but they are still hoisted

### What is hoisting? ###
Hosting is when the JS engine brings all declarations to top of their respective scope
- This isn't technically how it wowrks, but it is a decent enough mental model
- This happens to all declarations, but with two distinctions
  - `function` declarations have their _entire_ definition hoisted_ (body included)
  - `var` declarations are hoisted and then initalized to a value of `undefined` (implicitly) during the execution phases until a the code is reached that assigns a value

```javascript
// Before hoisting
hello()

function hello() {
  if (true) {
    console.log(x) // 'undefined'
    var x = 'hello';
  }
  console.log(x); // 'hello'
}
```
```javascript
// After hoisting
function hello() {
  var x;
  if (true) {
    console.log(x); // 'undfined'
    x = 'hello';
  }
  console.log(x); // 'hello'
}

hello();
```

### Temproaral Deadzone ###
As mentioned before, delcaratinos made with `let`, `const` and `class` are also hoisted, but they are not implicitly initalized to `undefined`
- Instead, these declarations have **NO** value, and are conisdered to be within the *temporal deadzone(
  - They remain here until the code that initalizes them is executed
  - As a result, trying to access these variables will throw a reference error

```javascript
// Before hoisting
console.log(x);
var x = 'hello';

console.log(y);
let y = 'world';

console.log(z);
```
```javascript
// After hoisting
var x;
let y; (temproal deadzone, no value)

console.log(x); // 'undefined'
x = 'hello';

console.log(y) // ReferenceError: Cannot 'access' 'y' before initialization (Look at the wording of this error)
console.log(z) // ReferenceEffor: z is not defined (notice how this is different. JS knows where a declaration is in the TDZ vs not defined)
```
### A note on function declarations ###
- Rememeber that function declarations have function scope
- Also remember that the *entire* function definition is hoisted
- These means something like the code below works
- With function expressions, they are not hoisted, and they throw a 'not defined' error instead of an initalization error

```javascript
// Before hoisting
function printHelloWorld() {
  return `${hello()} ${world()}`;
  
  function hello() {
    return 'hello';
  }
  
  function world() {
    return 'world';
  }
}

printHelloWorld(); // 'hello world'
```
```javascript
// After hoisting
function printHelloWorld() {
  function hello() {
    return 'hello';
  }

  function world() {
    return 'world';
  }
  
  return `${hello()} ${world()}`;
}
```
A note about class declaratins
- They are similar to variables declared with `let` and `const`
- They are hoisted, **but** their definitions are **not**

```javascript
// Before hoisting

let person = new Person('Brandon', 24); // ReferenceError: Person is not defined

class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}
```
```javascript
// After hoisting
class Person; (Living in TDZ)

let person = new Person('Brandon', 24); // ReferenceError: Person is not defined (similar to how function expression swork)

Person = class {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}
```
