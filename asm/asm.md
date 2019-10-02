```assembly
_add_a_and_b: # 建立一个新的帧
   push   %ebx # 将EBX寄存器里面的值, 写入_add_a_and_b这个帧. 因为后面要用到这个寄存器, 所以先把里面的值取出来, 用完再写回去. 此时ESP寄存器里面的地址会再减去4字节
   mov    %eax, [%esp+8] # 将ESP寄存器里面的地址加上8字节, 得到2的地址, 将2的地址写入EAX寄存器
   mov    %ebx, [%esp+12] # 取出3, 写入EBX寄存器
   add    %eax, %ebx # 相加, 将结果写入EAX寄存器
   pop    %ebx # 取出Stack最近写入的值(即EBX寄存器的原始值), 再将值写回EBX寄存器. ESP寄存器地址加4, 回收4个字节
   ret  # 终止当前函数的执行, 将运行权交还给上层函数. 也就是, 当前函数的帧将被回收

_main: # 在Stack上位main建立一个帧, 将Stack所指的地址写入ESP寄存器
   push   3 # 取出ESP寄存器里面的地址, 将其减去4个字节(32位指针占4字节), 将新地址写入ESP寄存器, 
   push   2 # ESP寄存器再减4字节
   call   _add_a_and_b # 调用函数
   add    %esp, 8 # 再回收8字节地址, 总共回收12字节
   ret
```

我们用到EBX就push EBX，而用到EAX却没push EAX: EAX 属于最频繁使用的通用寄存器，所以约定没有必要保留它的值 



## [为什么X86汇编中的mov指令不支持内存到内存的寻址？](https://www.cnblogs.com/wangchengfeng/p/3750961.html)

致同一时刻，CPU 只能对内存做一种访问的直接限制条件就是数据总线是单车道。