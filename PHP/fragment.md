# `file_exists()`和`is_file()`的区别
- `file_exists()`: 判断文件或目录是否存在, 执行效率低
- `is_file()`: 只判断文件名是否存在, 效率高
- `is_dir()`: 只判断目录是否存在

最好是单独使用

# PDO
[PDO manual](http://php.net/manual/en/class.pdo.php)
[不同的fetch类型](https://www.php.net/manual/zh/pdostatement.fetch.php)

### different between `query` and `execute`
`query`runs a standard SQL statement and requires you to properly escape all data to avoid SQL injections and other issues
`execute`runs a prepared statement allows you a bind parameters to avoid the need to escape or quote the parameters. **execute will also perform better if you are repeating a query multiple times**.

# include require
- `include`
- `include_once` 会先看看这个文件在前面有没有被`include`, 有的话就不再`include`
:warning: `include`过来的文件里如果包含要包含css, 写的路径应该是`include`那个文件到css的路径, 而不是被`include`的文件到css的路径
include在引入不存文件时产生一个警告且脚本还会继续执行，而require则会导致一个致命性错误且脚本停止执行
