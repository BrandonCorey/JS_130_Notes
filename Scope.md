### Declared Scope ###
Based on the syntax used to declare a variable

**Block Scope**
- `class`
- `let`
- `const`

**Function Scope**
Both of these variable types have their declarations hoisted to the top of a function (or program if in global scope)
- `function`
- `var`

```javascript
let x = 5; // block scope

if (true) {
  var q = 3; // functin scope
}

function test() {
  if (x === 5) {
    let y = 2; // block scope
    var z = 4; // function scope
    }
  
  console.log(z); // 4
  console.log(y); //ReferenceError: y is not defined
}

test();
```

### Visibiilty Scope ###
Based on where the variables are visible in the program

**Local Scope**
- Only visible within the block or function in which they are declared
  - Includes function and block scope

**Global Scope**
- Visible throughout the entire program

```javascript
let x = 5; // global scope

if (true) {
  var q = 3; // global scope
}

function test() {
  if (x === 5) {
    let y = 2; // local scope (block)
    var z = 4; // local scope (function)
    }
  
  console.log(z); // 4
  console.log(y); //ReferenceError: y is not defined
}

test();
```

### Lexical SCope ###
Refers scope refers to how the structure of your code determines what variables are accessible or inaccesbile at any point in the program.

- Inner Scope
- Outer Scope

These terms are relative depending on the surrounding structure of the code. Something can be outer scope to one statement while being inner scope to another.

```javascript
let x = 5; // outer scope of test

if (true) {
  var q = 3; // outer scope of test, outer scope of if statement
}

function test() {
  if (x === 5) {
    let y = 2; // inner scope of if statement
    var z = 4; // inner scope of test
    }
  
  console.log(z); // 4
  console.log(y); //ReferenceError: y is not defined
}

test();
```
