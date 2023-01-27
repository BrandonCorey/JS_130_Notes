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

NOTE: When using `require` for node modules, we do not need to specify the relative path. Node will always look in the directories `node_modules` directory

