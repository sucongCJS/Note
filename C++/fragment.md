# 常用

- 字符串和整数的转换
  - atoi() 参数是字符串指针
  - itoa

## C++编译运行过程

1. 预编译(预处理)(preprocessor): 展开包含的头文件(\*.h), 宏定义, 变成 \*.i 文件
`g++ -E .\test.cpp -o .\ycl.cpp`
2. 汇编: 把已经预编译的文件编译成汇编代码, 包括语法, 词法分析和一些优化操作
3. 编译: 变成目标代码, 即二进制文件(可以和汇编合成一个阶段)
4. 链接: 将单个编译后的文件链接成一个可执行程序(\*.exe). 预编译, 汇编, 编译都是对单个文件, 以一个文件为一个编译单元, 链接则是将所有关联到的编译后单元文件和应用到的库文件进行一次链接处理, 之前编译过的文件如果有用到其他文件里面定义到的函数, 全局变量, 在这个过程中都会进行解析.

## 文件扩展名描述
- .c	C 源文件
- .C、.cc、.cp、.cpp、.cxx 和 .c++	C++ 源文件
- .i	预处理的源文件
- .ii	预处理的 C++ 源文件
- .o	对象文件
- .s	汇编程序文件
- .S	未预处理的汇编程序文件
- .so	共享对象或库文件

</br></br><b>Reference List</b>:
- [C++ 编译，运行过程 详解](https://blog.csdn.net/yinzhuo1/article/details/47069201)
- [文件类型](https://www.ibm.com/support/knowledgecenter/zh/SSXVZZ_13.1.3/com.ibm.xlcpp1313.lelinux.doc/getstart/inputoutput_files.html)
