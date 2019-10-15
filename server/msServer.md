# AD

**Active Directory** (AD) is a Microsoft product that consists of several servicefs that run on [Windows Server](https://searchwindowsserver.techtarget.com/definition/Microsoft-Windows-Server-OS-operating-system) to manage permissions and access to networked resources.

Active Directory stores data as objects. An object is a single element, such as a user, group, application or device, such as a printer. Objects are normally defined as either resources -- such as printers or computers -- or security principals -- such as users or groups.

活动目录是一种数据库(基于文件的数据库, 不同于Oracle, SQL Server, 是一种轻量的数据库), 可以对Domain(域)中可管理的对象进行合理的存放, 

![1570692259026](D:\Note\server\Untitled.assets\1570692259026.png)

Active表示所有的属性字段并不是固定的

AD数据库文件默认保存在 C:\Windows\NTDS:

- ntds.dit 主数据文件
- edb0000x.log 事务日志 (检查点文件, 断点重启恢复, 写入快, 所以可以先把操作记录到日志中, 再在主数据文件中修改)
- ebd.chk 检查点文件(断电的时候可以记录上一次哪个文件只写入到于日志中, 但还没有写入到主数据文件中, 然后可以进行恢复)
- edbres000x.jrs 预留文件(硬盘写满之前写到这个文件)

# OU

An organizational unit (OU) is a subdivision within an [Active Directory](https://kb.iu.edu/d/ambu) into which you can place users, groups, computers, and other organizational units. 

You can create organizational units to mirror your organization's functional or business structure. 

建议扁平化

在domain里

# DC

域控制器, 存放AD数据库的服务器, 运行ADDS(Active Directory Domain Service)服务, 卸载ADDS之后服务器就变成普通服务器了

A **domain controller** is a **server** that responds to authentication requests and verifies users on computer networks. 

Domains are a hierarchical way of organizing users and computers that work together on the same network. The domain controller keeps all of that data organized and secured.

一个Domain中可以有多个DC

同一个域中的每台DC上的AD数据库一样, 且会定时或在发生改变时自动在DC之间相互同步复制, 同步复制的频率和时间窗口可以配置和定义

## RODC

> Read Only Domain Controller

- 适合部署在没有本地管理需求的远程分支机构
- 不允许在RODC本地对数据库做出更改操作
- RODC保存域控制器AD数据库的只读副本

## GC

> Global Category Server 全局编录服务器

- GC是一种特殊的域控制器, 一个域至少部署一台
- GC用于多域环境中和其他域进行数据同步(但并不是同步全部数据, 通常需要同步的数据仅占AD数据总量的5%~10%), 以便优化Exchange Server等应用的全局或跨域搜索的效率

# Domain

![1570692281294](D:\Note\server\Untitled.assets\1570692281294.png)

比域更松散的结构为工作组, 只能用于小的组织

Domain存放于AD中, AD运行于DC中

![1570693277976](D:\Note\server\Untitled.assets\1570693277976.png)



## 域中的角色

- DC
- 域内的成员服务器
- 域内的终端 计算机

## Forest

![1570696201560](D:\Note\server\Untitled.assets\1570696201560.png)

# Domain, Global, Universal Group

Domain local group可以包含任何一种universal group， global group， 本domain内的其他local group， 本forest内的任何domain的account



Global group可以在它所在的domain内使用，还有其内的成员服务器或工作站，还有信任本domain的domain中使用。在所有这些地方，你可以赋予global group权限，也可以让global group成为local group的成员。然而，global group仅能包含它所在domain的用户帐户



Universal group是包含本forest内的任何domain内的用户，组，计算机的security goup或distribution group。你可以给universal group在本forest中的任何domain中的资源上赋权限。

# Site





# vit

- DFS
- print queue
- 