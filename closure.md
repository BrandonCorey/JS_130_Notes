### Closure ###
Closures are created when you define a function or method. The closure essentially closes over its environment -- what's in lexical scope.
- So all the things *in scope* of the function are part of the **closure**, along with the variables within its function defintion
- Note: Even if those variaables aren't in lexical scope where the inovcation takes place, the function can still access them

Closure --> function definition + variables in lexical scope of the function
- Does not include variables in scope where the invocation takes place *unless* those variables were also in the definition's scope

The lesson: **where you invoke the function doesn't dictate what it has access to, where you define it does**

Note: A "closure" will store references to all variables referred to within its function definiton
- Launch school tells us to think about this as an envelope object that is attached to the function that stores the references
