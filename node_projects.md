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
- **packages are made up of modules**
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

Packages should almost always be installed locally so you/npm can install the correct version of the package for your project
- A version installed globally may be compatible with one project, but not another

Some packages don't typically require different versions for different projects and be installed globally
- Examples of this are `jest` and `heroku`
- These can be installed using the global flag `npm install heroku -g` or `npm install jest -g`
  - NOTE: You may need root privelages to install a global package i.e (`sudo npm install jest -g`)
- To uninstall all global packages, use `rm -fr node_mudles package.json package-lock.json`
  - global packages for Ubuntu are stored in `/usr/local/lib/node_modudles`

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
While Node will add a `package.json` automatically when you install a package, it can also be created manually
- You can manually add a `dependencies` key with the relevent information of the module you want to install
- After you add your `dependencies`, you can use `npm install` to find the version you specified and install it into `node_modules`
- Can also do it automatically using `npm install <packagename> --save`
  - `--save` flag tells npm to save the package to the `dependencies` list in `package.json`. Can also use `-S` flag

Some packages may only be relevant in the context of a development enviroment, and not suitable for production (e.g `eslint`)
- There is a section within a `package.json` for these dependecies as well called `devDependencies`
- Can manually add this to a `package.json` or use `npm install <packagename> --save-dev`
### `package-lock.json` ###
Installing modules will create a `package-lock.json`, which will contain specific info about which minor version and patch of which version your project is using
  - The `package-lock.json` will also show all the dependencies that your dependency has
  - NOTE: Verson is considered the major number that we specify in our `package.json`, but Node will determine the minor version and patch for us
    - Ex) Version 4.17.1 --> Major version: 4, Minor version: 17, Patch version: 1
  - The `package-lock.json` file is important as the next time `npm install` is ran, it will install the exact depencies needed, down to patch number
    - This is incredibly helpful if a team of developers are working on something

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
    "lodash": "^4.17.15",
    "morgan": "1.9"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "eslint": "^8.32.0"
  }
}
```

### Global vs Local executable packages ###
- To run an executable globally, call it using its name i.e `eslint <filename.js>`
- To run an executable locally, call it using npx + its name i.e `npx esilnt <filename.js>`
  - **Note:** if you don't have a local version of a package installed, npx will check globally, and if not found, downloads a temporary version to use

### Deleting a dependency ###
- Use `npm uninstall <packagename>` (i.e `npm uninstall lodash`)
- To uninstall and remove from `package.json` dependencies, use `npm uninstall <packagename> --save`
- To uninstall from dev dependencies, use `npm uninstall <packagename> --save-dev`
- Can also use `npm prune` to remove any packages from `node_modules` that are not listed in the `package.json`
