## JS Engine Phases ##

### Creation ###
- Takes note of all declarations in program
  - Also takes not of their scope
- Runs through program line by line, top down
- Note: This where syntax errors take place

### Execution ###
- Runs programs line by line
- Doesn't care about declarations, does care about initalizations and definitions
- Does *hoisting* for all declarations (moves them to top of scope)
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
### Reminder tha hoisting is not actually real ###
- In reality, JS goes through creation phase from the top down
- It takes note of all declarations and their scope
- During execution phase, it executes from the top down as well, but is aware of all declarations and executes them based on specific rules the engine has
  - Some of these rules function declarations allowed to be called before they are executed
  - Another rule is var being initalized to undefined by default

### If a function declaration and var declaration share same name ###
- If they share the same name, the `var` declaration is discarded, but its initalized value still remains
  - This results in a simple reassignment at the point in the code where the variable was initalized
  - This also happens if two `function` declarations share the same name, OR two `var` declarations

```javascript
// Before hoisting
var foo = function() {
  console.log('bye');
}

foo(); // logs 'bye'

var foo = 5;

function foo() {
  console.log('hello')
}
```
```javascript
// After hoisting
function foo() {
  console.log('hello')
}

foo = function() {
  console.log('bye');
}

foo();

foo = 5;
```
