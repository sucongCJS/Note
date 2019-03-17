# 日常操作
## kill zombie
```shell
ps -A -o stat,ppid,pid,cmd | egrep '^[Zz]';
kill -9 pid
# or do via script
ps -A -o stat,ppid,pid,cmd | grep -e '^[Zz]' | awk '{print $2}' | xargs kill -9

```
## top
```shell
# see the specific pid
top -d 1 -p 29907
```
STAT状态常见的状态字符
- D 无法中断的休眠状态（通常 IO 的进程）；
- R 正在运行可中在队列中可过行的；
- S 处于休眠状态；
- T 停止或被追踪；
- W 进入内存交换  （从内核2.6开始无效）；
- W 无驻留页 has no resident pages 没有足够的记忆体分页可分配。
- X 死掉的进程   （基本很少見）；
- Z 僵尸进程；
- < 优先级高的进程
- N 优先级较低的进程
- L 有些页被锁进内存；
- s 进程的领导者（在它之下有子进程）；
- l 多进程的（使用 CLONE_THREAD, 类似 NPTL pthreads）；
- \+ 位于后台的进程组；

- [more kill skills](https://www.jianshu.com/p/5ab557f8a6bf)

## Aria2下载
- [命令简介](https://blog.csdn.net/gatieme/article/details/44782801)
- [命令介绍2](http://www.yourownlinux.com/2013/10/speed-up-file-downloads-in-linux-using-aria2-download-manager.html)

## 解压
tar
```bash
# extract
tar -zxvf FileName.zip -C /zzz/bbs
# 保存到的目录要存在, 不像cp一样没有会给你创建
# -z支持gzip解压文件

# compress
tar zcvf CompressedFile.tar File
```


# 零碎知识
## 文件符号
`ls`时文件后面总是有各种各样的符号, 他们的意思是:
*: 可执行文件
/: 目录
=: 套接字
@: 符号链接(软连接)
|: 管道文件

# wine uninstall software:
wine uninstaller
