# PHP Variables
## PHP Variables Scope
- local
> A variable declared within a function has a LOCAL SCOPE and can only be accessed within that function

ways to access a global variable
  - `glocal`
  - PHP stores all global variable in an array called `$GLOBALS[index]`, you can use `$GLOBALS[VAR_NAME]`

- global
> A variable declared outside a func has GLOBAL SCOPE and can only be accessed outside a function, which is different to Python.
- static
> Normally, when a function is completed/executed, all of its variable are deleted, we can use the `static` keyword to prevent this happen.

# echo and print statement
`echo` has no return value
`print` has a return value of 1 so it can be used in expressions.
`echo` is faster than `print`

# PHP Date Type
var_dump()
gettype()
settype()

# Class
## PDO
[PDO manual](http://php.net/manual/en/class.pdo.php)

### different between `query` and `execute`
