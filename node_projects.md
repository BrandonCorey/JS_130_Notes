## Node Pojects ##
Should always created a new local directory, new github repository, and new Git repository for projects
- Make sure that all directories and parent directories **do not have spaces**

### Necessary files/directories for now ###
- `test` directory for storing all of our test files
- `lib` directory for storing our source code
- `.gitignore` file containing the text `node_modules` (this file is hidden)
- `README.md` containg whatever text we want to describe project

Example:
```
todolist_project
├── README.md
├── lib
│   ├── todo.js
│   └── todolist.js
└── test
    └── todolist.test.js
```

### Node Packages ###
Packages of code that can be downloaded, installed, and used in your code or system
- Some can be imported into programs
- Some can be used from the command line
- Some can do both

The `npm` command is used to manage packages

### Examples of packages I've alreasy used ### 
- `eslint` (command-line)
- `jest` (command line)
- `readline-sync` (imported into program)

Things like `readline` are programming interfaces, it is a module that we require and allows us to use its methods/functions

Things like `jest` and `eslnt` are command line executables

NOTE: When using `require` for node modules, we do not need to specify the relative path. Node will always look through your `node_modules` directory

### Local vs Global Packages ###
Local packages are installed to your project directory
- They will be installed in your `node_modules` directory. If you do not have one, one will be created
  - This is why no parent directories should have a node modules folder, because node will use that instead of creating a new one

```javascript
const _ = require('lodash'); // lodash library is an object with methods
const chunk = require('lodash/chunk'); // Can import functions we want directly (faster loading, less memory used)

chunk = require('lodash').chunk; // Note: Not all libraries independently export their functions like lodash. We can use this syntax for those
                                 // This still imports all the methods, but they get garbage collected quickly

console.log(_.chunk([1, 2, 3, 4, 5, 6, 7, 8], 2));
// logs [[1, 2], [3, 4], [5, 6], [7, 8]]
console.log(chunk([1, 2, 3, 4, 5, 6, 7, 8], 2));
```

### `package.json` and `package-lock.json` ###
The `package.json` file contains important information about your Node project, including all of your projects dependncies
- A `package.json` can be created using `npm init`

### `package.json` ###
While Node will add a `package.json` automatically when you install a package, it is generally better practice to create it yourself
- You can manually add a `dependencies` key with the relevent information of the module you want to install
- After you add your `dependencies`, you can use `npm install` to find the version you specified and install it into `node_mudles`
### `package-lock.json` ###
The above process will also creates a `package-lock.json`, which will contain specific info about which minor version and patch of which version your project is using
  - The `package-lock.json` will also show all the dependencies that your dependency has
  - NOTE: Verson is considered the major number that we specify in our `package.json`, but Node will determine the minor version and patch for us
    - Ex) Version 4.17.1 --> Major version: 4, Minor version: 17, Patch version: 1

```json
// package.json example
{
  "name": "todolist",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "directories": {
    "lib": "lib",
    "test": "test"
  },
  "dependencies": {
    "express": "4",
    "http-errors": "1",
    "morgan": "1.9"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```
