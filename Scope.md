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
