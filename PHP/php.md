# 入门基础
## PHP Variables
### PHP Variables Scope
- local
> A variable declared within a function has a LOCAL SCOPE and can only be accessed within that function

ways to access a global variable
  - `glocal`
  - PHP stores all global variable in an array called `$GLOBALS[index]`, you can use `$GLOBALS[VAR_NAME]`

- global
> A variable declared outside a func has GLOBAL SCOPE and can only be accessed outside a function, which is different to Python.
- static
> Normally, when a function is completed/executed, all of its variable are deleted, we can use the `static` keyword to prevent this happen.
## 常量
```php
define('PRICE', 100);
echo PRICE;
```
## 作用域
超级全局变量:
- $GLOBALS: 所有全局变量数组
- $_SERVER: 服务器环境变量数组
- $_REQUEST: 包括$_GET, $_POST, $_COOKIE

## 从控制结构或脚本跳出
`exit`终止PHP的执行


## echo and print statement
`echo` has no return value
`print` has a return value of 1 so it can be used in expressions.
`echo` is faster than `print`

# PHP Date Type
var_dump()
gettype()
settype()


# 数据的存储和检索
## 使用不同索引的数组
### 使用循环语句
```PHP
foreach ($prices as $key => $value){
  echo $key."-".$value."<br />";
}

while ($element = each($prices)){
  echo $element['key'].'-'.'$element['value'].'<br />';
}

```

# Class
## PDO
[PDO manual](http://php.net/manual/en/class.pdo.php)

### different between `query` and `execute`
`query`runs a standard SQL statement and requires you to properly escape all data to avoid SQL injections and other issues
`execute`runs a prepared statement allows you a bind parameters to avoid the need to escape or quote the parameters. **execute will also perform better if you are repeating a query multiple times**. {qe1}



<br/><br/>reference list:
qe1 [query vs execute](https://stackoverflow.com/questions/4700623/pdos-query-vs-execute)
