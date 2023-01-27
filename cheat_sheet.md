## Things to remember ##
### Node project standards ###
- a `lib` directory with your source code
- a `test` directory with your tests
- a `dist` directory with your transpiled ES5 code
- an `index.js` file acting as your main file
- a `.gitignore` file containg `node_modules` inside
- a `README.md` acting as your readme

### npm ###
- `npm init` will add a `package.json`
- `npm install` will install any `dependencies` listed in your `package.json` and update your `package-lock.json` with info on them
- `npm install <packagename> --save` will install a package and add it to your `dependecies` in `package.json`
- `npm install <packagename> --save-dev` will install a package and add it to your `devDependencies` in `package.json`
- `npm install <packagename> -g` will install a package globally (will be located in `/usr/local/lib/node_modules`)
- `rm -fr node_mudles package.json package-lock.json` to remove global node modules and related files
- `npx <packagename>` this will run an executable package

Many packages can be imported to your code instead of executed, like `readline` and `lodash`
- Can access specific methods depending on how a library within a package is organized
```javascript
const _ = require('lodash'); // entire library
const chunkDirect = require('lodash/chunk'); // Only chunk function (ignores everything else in library)
const chunkIndrect = require('lodash').chunk; // entire library, immediately assign method, rest will be GC'd (good for less organized libraries)
```

The scripts inside of your `package.json` can be used to store `npm` commands that may need to be run a lot

### Babel ### 
- `npm install --save-dev @babel/core @babel/cli` to install
- `npm install --save-dev @babel/preset-env` to install preset (plugin) transpiles ES6+ to ES5
- `npx babel lib --out-dir dist --preset=@babel/preset-env` to transpile js files in `lib` to ES5, and output them to a `dist` directory in the same directory as `lib`
