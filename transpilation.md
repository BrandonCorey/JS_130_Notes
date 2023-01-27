## Transpilation ##
Transpilation is the process of converting source code written in one language into another language with a similar level of abstraction to the original code.
- In JS, this often means taking code written in a superset of JS and rewriting it in JS
  - This typically means converting ES6+ code to ES5
  - We do this so new JS features work in all runtime enviroment

### Babel ###
This is by far the best and most poppular javaScript transpiler

To install:
- `npm install --save-dev @babel/core @babel/cli`
  - Recommended to install babel locally despite being a command-line utility
  - `@babel/core` is the core library that provides us the ability to transpile
  - `@babel/cli` is the cli provided to us to interface with the library

We need to install the `env` preset (a type of plugin) to transpile our code to ES5:
`npm install --save-dev @babel/preset-env`
- The `env` preset is used to transpile JS code to ES5

Finally, to **transpile our ES6+ to ES5**:
`npx babel lib --out-dir dist --preset=@babel/preset-env`
- This will transpile all of our js files in the `lib` directory of our current directory
- It will output files of the same name to a `dist` directory
