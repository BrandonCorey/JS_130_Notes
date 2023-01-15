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
// Before
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
