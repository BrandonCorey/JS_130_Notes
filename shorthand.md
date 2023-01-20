### Concise Property Initalizaers ###
- Allows you to use a variable as a property value and automatically assigns the name as well
```javascript
function createObj(prop1, prop2) {
  return {
    prop1, // instead of prop1: prop1
    prop2, // instead of prop2: prop2
  }
}
```

### Concise Methods ###
- Allows you to define methods in a more concise way
```javascript
let obj = {
  test() { // instead of test: function() {}
    console.log('test');
  }
}
```

### Object Destructuring ###
- Allows you to extract object properties for variable assignment
- Unlike array destructuring, you access the propeties based on the names, not the order, so any order can be used
- Can initalize variable with different name than property
```javascript
let obj = {
  name: 'Brandon',
  age: 24,
  degree: 'Economics',
}

let { name, age } = obj;
{ age, name } = obj; // any order
let { degree: major } = obj; // declaring a variable name major with value of obj.degree
console.log(name, age, major); // "Brandon 24 Economics"

function test({ name, age, degree }) {
  console.log(name);
  console.log(age);
  console.log(degree);
}

test(obj);
```

### Array Destructuring ###
- Similar to object restructuring, but relies on order of elements for assign
- Can skip over non-relevent elements by exluding the between commas, like this: `, ,`
```javascript
let arr = [1, 2, 3, 4, 5];
let [ first, second, , , fifth ] = arr;

console.log(first, second, fifth);
```

### Spread Syntax ###
- Used to spread elements of an array or object into serperate itmes
- Will turn something like `[1, 2, 3]` into `1, 2, 3`
- Can **also** spread objects, but must put back into an object (unlike an array)
  - NOTE: Does not copy the object's prototype, only copies enumerable properties
```javascript
let arr = [1, 2, 3];
let bar = { a: 4, b: 5 }

let max = Math.max(...arr); // max is 3

let arrCopy = [...arr, {...bar}];
console.log(arrCopy); // [ 1, 2, 3, { a: 5, b: 5 } ]
```
### Rest syntax ###
- Acts as the opposite of spread syntax
- Takes seperate items and compacts them to a single entitiy
- Most common use it to take a variable amount of function arguments
- Can use `rest` as name or any other legal name, but `rest` will ovveride any property names and act as the rest operator, where other names will not
```javascript
let arr = [1, 2, 3, 4, 5, 6];
let foo = { a: 4, b: 5 , c: 6}
let [ one, ...rest] = arr;
let {a, ...others} = foo;

console.log(one); // 1
console.log(rest); // [2, 3, 4, 5, 6]
console.log(a); // 4
console.log(others); // { b: 5 , c: 6 }

function test(...args) { // This syntax puts the args into an array
  return args.reduce((sum, val) => sum + val);
}

test(1, 2, 3); // 6
```
