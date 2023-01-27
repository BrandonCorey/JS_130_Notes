## NPM scripts ##
We can add scripts to our `package.json` within the "scripts" object

### Babel script ###
Lets make using babel easier:

We can add `npx babel lib --out-dir dist --presets=@babel/preset-env` to the script called `babel`
- Note, we can exclude `npx` within scripts, as they will automatically run locally as long as your package is installed locally

```json
{
  "name": "todolist_project",
  "version": "1.0.0",
  "description": "This repo is to learn how to format node projects",
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
    "test": "echo \"Error: no test specified\" && exit 1",
    "babel": "babel lib --out-dir dist --presets=@babel/preset-env"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/BrandonCorey/todolist_project.git"
  },
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/BrandonCorey/todolist_project/issues"
  },
  "homepage": "https://github.com/BrandonCorey/todolist_project#readme",
  "devDependencies": {
    "@babel/cli": "^7.20.7",
    "@babel/core": "^7.20.12",
    "@babel/preset-env": "^7.20.2",
    "eslint": "^8.32.0"
  }
}

```
