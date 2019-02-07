## Samba 简介
> Samba（SMB是其缩写） 是一个网络服务器，用于Linux和Windows共享文件之用；Samba 即可以用于Windows和Linux之间的共享文件，也一样用于Linux和Linux之间的共享文件；不过对于Linux和Linux之间共享文件有更好的网络文件系统NFS，NFS也是需要架设服务器的；


## 识别 Samba 后台程序
> Linux 服务器通常作为守护程序（daemon） 来实现，这一词源于希腊神话，其中守护神（daemon）是超自然生物。(BTW: linux中以d结尾的多是守护进程，如httpd，mysqld，crond等。守护进程多是无输出状态的，伴随着系统的启动而启动，系统的关闭而结束，在后台等待执行的进程)Linux 守护程序在后台运行以便执行一些有用的任务。Samba 服务器套件由几个守护程序组成，包括 **smbd**、**nmbd** 和 **winbindd**。swat 程序是另外一个 Samba 服务器，但是其通常都是从一个超级服务器运行，因此在技术上不是守护程序

## 了解 smbd
smbd 程序提供 Samba 的大部分核心功能。其职责包括：
- **提供文件和打印机共享**。此功能可以说是一个最重要的 Samba 职责，smbd 执行此功能。smb 是Samba 的主要启动服务器，让其它机器能知道此机器共享了什么
- **验证用户**。smbd 针对本地数据库验证用户或传递验证请求到另一台计算机。如果您的 Samba 服务器被配置为域控制器，则 smbd 还可从其他计算机响应验证请求。（在 设置您的安全模式 中将描述工作组和域配置）。
- **提供时间服务**。Samba 可以告诉其他计算机当前的时间；smbd 可处理此细节。

## [global]参数
`security = user`
> 这里指定samba的安全等级. 关于安全等级有四种：
- share：用户不需要账户及密码即可登录samba服务器
share在新版已经被废弃了, 要实现相同的效果应该用
```shell
security = user
map to guest = Bad User
```
- user：由提供服务的samba服务器负责检查账户及密码（默认）
- server：检查账户及密码的工作由另一台windows或samba服务器负责
- domain：指定windows域控制服务器来验证用户的账户及密码。

`passdb backend = tdbsam`
> passdb backend （用户后台），samba有三种用户后台：smbpasswd, tdbsam和ldapsam
- **smbpasswd**：该方式是使用smb工具smbpasswd给系统用户（真实用户或者虚拟用户）设置一个Samba 密码，客户端就用此密码访问Samba资源. smbpasswd在/etc/samba中，有时需要手工创建该文件
- **tdbsam**：使用数据库文件创建用户数据库。数据库文件叫passdb.tdb，在/etc/samba中。passdb.tdb用户数据库可使用smbpasswd –a创建Samba用户，要创建的Samba用户必须先是系统用户。也可使用**pdbedit**创建Samba账户
pdbedit参数很多，列出几个主要的(:warning:必须用root权限)：
`pdbedit -a username`：新建Samba账户
`pdbedit -x username`：删除Samba账户
`pdbedit -L`：列出Samba用户列表，读取passdb.tdb数据库文件.
`pdbedit -Lv`：列出Samba用户列表详细信息
`pdbedit -c “[D]” -u username`：暂停该Samba用户账号
`pdbedit -c “[]” -u username`：恢复该Samba用户账号。
- **ldapsam**：基于LDAP账户管理方式验证用户。首先要建立LDAP服务，设置“passdb backend = ldapsam:ldap://LDAP Server” load printers 和 cups options 两个参数用来设置打印机相关。

## 清楚Samba和其配置文件
清除应该删除配置文件，但Samba服务器的配置由包samba-common跟踪，而不是samba。是的，这有点令人困惑。
因此，尝试清除并重新安装这两个软件包：
```bash
sudo apt-get purge samba samba-common
sudo apt-get install samba
```

# 命令操作
## 用户操作
### 添加用户
只能添加系统已经存在的用户, 如
`sudo smbpasswd -a jason`
'jason'必须是存在于系统中的用户

## 启动关闭Samba命令
```shell
/* 启动 */
[root@localhost ~]# /etc/init.d/smb start

/* 停止, 重启 */
[root@localhost ~]# /etc/init.d/smb stop
[root@localhost ~]# /etc/init.d/smb restart

/* 对于所有系统来说，通用的办法就是直接运行smb 和nmb；当然您要知道smb和nmb所在的目录才行；如果是自己编译的Samba ，您应该知道您把Samba放在哪里了； */
[root@localhost ~]# /usr/sbin/smbd
[root@localhost ~]# /usr/sbin/nmbd

/* 查看服务器是否运行起来了，则用下面的命令； */
[root@localhost ~]# pgrep smbd
[root@localhost ~]# pgrep nmbd

/* 关掉Samba服务器，也可以用下面的办法，大多是通用的；要root权限来执行； */
[root@localhost ~]# pkill smbd
[root@localhost ~]# pkill nmbd
```

## 查看Samba 服务器的端口及防火墙
查看这个有何用呢？有时你的防火墙可能会把smbd服务器的端口封掉，所以我们应该smbd服务器所占用的端口

<br/><br/>
reference list:
- [配置 samba 服务器, 参数意义](http://wiki.jikexueyuan.com/project/linux/samba.html)
- [Linux就该怎么学, 参数](https://www.linuxprobe.com/chapter-12.html)
- [我如何重新安装Samba？](http://www.kbase101.com/question/1418.html)
- [Samba角色 和 三个守护程序详解](https://www.ibm.com/developerworks/cn/linux/l-lpic3-310-2/)
- [Samba权限设置, Samba介绍, 端口防火墙](https://my.oschina.net/laopiao/blog/161648)
