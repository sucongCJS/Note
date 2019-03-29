# `file_exists()`和`is_file()`的区别
- `file_exists()`: 判断文件或目录是否存在, 执行效率低
- `is_file()`: 只判断文件名是否存在, 效率高
- `is_dir()`: 只判断目录是否存在

最好是单独使用

# PDO
[PDO manual](http://php.net/manual/en/class.pdo.php)

### different between `query` and `execute`
`query`runs a standard SQL statement and requires you to properly escape all data to avoid SQL injections and other issues
`execute`runs a prepared statement allows you a bind parameters to avoid the need to escape or quote the parameters. **execute will also perform better if you are repeating a query multiple times**. {qe1}
