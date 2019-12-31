# 概念

## CLR

> common language runtime

runs the code and provides services that make the development process easier. 

## Windows Server 2016

- maximum number of mounted drives: 
- maximum of logical processors without Hyper-V: 640

### standard edition

- maximum number of supported **processor sockets**(the connector on the motherboard that houses a CPU and forms the electrical interface and contact with the CPU): 64

### datacenter edition

- 

essential edition

- not included Hyper-V 

## Storage tiering

> a way to assign different categories of data to various types of storage media with the objective of reducing the total cost of storage. 

## Logical processor

> **Logical** cores are the number of Physical cores times the number of threads that can run on each cores. This is known as HyperThreading. 

 If I have a computer that has a 4-core **processor**, runs two threads per core, then I have a 8 **logical processors**.

## P2P network

There is no centralized user management, any user who wants access to resources on another computer will need to have an account on that specific computer. So if a user wants access to files on 10 different computers then that user will need 10 separate user accounts.

## User Mode

 在用户态，代码不具备直接访问硬件或者访问内存的能力，而必须借助操作系统提供的可靠的，底层的APIs来访问硬件或者内存。由于这种隔离带来的保护作用，用户态的代码崩溃（Crash），系统是可以恢复的。我们大多数的代码都是运行在用户态的。

隔离保护，使得系统更稳定。

## Privilege mode

特权模式允许容器内的root拥有外部物理机root权限，而此前容器内root用户仅拥有外部物理机普通用户权限。

使用特权模式启动容器，**可以获取大量设备文件访问权限**。

当控制使用特权模式启动的容器时，docker管理员可通过mount命令将外部宿主机磁盘设备挂载进容器内部，**获取对整个宿主机的文件读写权限**，此外还可以**通过写入计划任务等方式在宿主机执行命令**。

## HKEY

### HKEY_LOCAL_MACHINE

- Contains information on every hardware component in the server
- Includes information about whatdrivers are loaded and their version levels, what IRQ lines are used, setup configurations, the BIOS version, and more

#### IRQ

> interrupt request line

IRQs are [hardware](https://www.webopedia.com/TERM/H/hardware.html) lines over which [devices](https://www.webopedia.com/TERM/D/device.html) can send [interrupt](https://www.webopedia.com/TERM/I/interrupt.html) signals to the [microprocessor](https://www.webopedia.com/TERM/M/microprocessor.html). 

## Plug and Play

- The ability to automatically detect
  and configure newly installed hardware devices
- Most devices universally support Plug and Play

# AD

**Active Directory** (AD) is a Microsoft product that consists of several services that run on [Windows Server](https://searchwindowsserver.techtarget.com/definition/Microsoft-Windows-Server-OS-operating-system) to manage permissions and access to networked resources.

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
- GC用于多域环境中和其他域进行数据同步(但并不是同步全部数据, 通常2需要同步的数据仅占AD数据总量的5%~10%), 以便优化Exchange Server等应用的全局或跨域搜索的效率

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

# DNS

> 域名服务器 Domain Name System

zone: tables are associated with partitions in a DNS server

- Forward lookup zone: 域名->ip

- Reverse lookup zone: ip->host name

Host(A):IP v4

Host(AAAA):IP v6

## primary DNS server

## secondary DNS server

- read-only
- 从primary DNS server 复制
- 负载均衡
- 热切换, 服务器崩了可以切换到另一台

如果一片区域有较多服务请求, 可以一台primary配合几台secondary

如果一大片区域都有服务请求, 可以多态primary

## stub zone

相当于目录, 只保留概括性的信息, 概括域内的信息, 先到这里找, 如果有要的东西再到域里仔细找

## round robin

ip不同的服务器用同样的host name, 负载均衡

## forwarder

找不到域名, 到父级DNS找

# DHCP

> dynamic host configuration protocal

根据设备设置ip回收时间(leasing duration)(公共场合的使用得多, 移动设备回收时间短), 防止ip分完了, 新的设备没有ip可以分

# NIC Teaming

网卡组队

# IIS

> internet information services

application pools 可以开多个iis



## Server Core Nano Server

最小版本      

## Demilitarized zone

## User Account Control

## Account Policies

### Kerberos security

认证系统 双向认证

## BitLocker Drive Encryption

整个硬盘加密

## Event viewer

记录系统所有的操作





第三章 域

第四章 文件系统, 权限

 

chkdsk





