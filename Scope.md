### Declared Scope ###
Based on the syntax used to declare a variable

**Block Scope**
- `class`
- `let`
- `const`

**Function Scope**
- `function`
- `var`

```javascript
let x = 5; // block scope

if (true) {
  var q = 3; // function scope
}

function test() { // function scope
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

function test() { // global scope
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
let x = 5; // outer scope of test, outer scope of if statement

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

### When to use ###
- Use declared scope when you're talking about how an identifier is declared.
- Use visibility scope when you're talking about the visibility of a specific identifier.
- Use lexical scope when you want to talk about whether something is "in scope" -- that is, whether it is available for use.
