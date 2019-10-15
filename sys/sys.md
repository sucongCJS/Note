# Legacy BIOS 和 UEFI BIOS 的区别
![](https://phoenixts.com/wp-content/uploads/2015/05/uefivslegacy.png)
UEFI BIOS 可以说是legacy BIOS的继承者

## BIOS
> Basic Input/Output System

## UEFI
> Unified Extensible Firmware Interface **统一可扩展固件接口**, **统一可延展韧体介面**
> ![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Efi-simple_zh-cn.svg/450px-Efi-simple_zh-cn.svg.png)

UEFI BIOS 并不是开机时第一个被执行的程式

## 启动电脑原理
1. BIOS由主机板上的快闪记忆体(flash memory)执行, 并将晶片组和记忆体系统初始化
2. BIOS把自己从快闪记忆体中解压缩到系统的主记忆体, 并从那边开始执行
3. ...

## BIOS 韧体
> 由于BIOS与硬件系统整合在一起(将BIOS程式指令烧录在IC中), 所以有时候也被称为韧体
> 最初BIOS是保存在ROM中的, 无法被修改. 后改为存储在EEPROM或快闪记忆体中, 使得BIOS可以被更新

## BIOS与CMOS的关系
> CMOS是计算机上另一个重要的存储器。之所以提到它，是因为BIOS程序的设置结果就保存在CMOS中。而且，在BIOS程序引导计算机启动后，计算机需要载入CMOS中的用户信息和常规设置后才能正常使用。UEFI系统则多用NVRAM储存设定

## BIOS与CMOS的区别
> 二者的区别是，BIOS是储存在唯读记忆体（EEPROM），而CMOS为随机存储器（RAM）；BIOS中存储的是程序，而CMOS中存储的是普通信息。
> EEPROM即是我们常用的随身碟和各类记忆卡，因此我们可以更新BIOS，其内容亦能在断电后保存。
> CMOS RAM的内容在断电会消失。所以，把主机板的电池拆出，便可重置其内容。另外，拆出电池也会重设时间。UEFI多使用NVRAM储存设定资料，主板电池没有电量会导致时间不正确，可能不会导致UEFI设定值遗失。可通过主板的有关Jumper重设UEFI设定

## 统一可延伸韧体介面(UEFI)和BIOS
> UEFI是模块化, C语言风格的参数堆栈传递方式, 动态链接的形式构建的系统, 比BIOS更易于实现, 容错纠错特性更强.
> EFI Byte Code是一组专用于EFI驱动程序的虚拟机器语言，必须在EFI驱动程序运行环境（Driver Execution Environment，或DXE）下被解释运行。采用EBC编写的EFI驱动程式拥有**平台无关性**
> BIOS多使用CMOS晶片保存BIOS设定值与硬体侦测资料，CMOS保存资料需要电力供应，如果主板上的CMOS电池已没有电量，那么在电脑断电后，CMOS中储存的资料会遗失，且系统时钟无法运作。UEFI多采用NVRAM储存韧体设定及硬体侦测资料

## 统一可延伸韧体介面（UEFI）和操作系统
> UEFI在概念上非常类似于一个低阶的操作系统, 并且具有操控所有硬件资源的能力.

## 统一可延伸韧体介面（UEFI）的组成(x64)
- **Pre-EFI初始化模块**:
开机时最先执行, 完成记忆体的初始化工作, 然后载入UEFI DXE
- **EFI驱动程序执行环境(DEX)**:
DXE被载入运行时, 系统才有枚举并加载其他UEFI驱动程序的能力
- **EFI驱动程序**
- **兼容性支持模块(CSM)**
**CSM**是在x86平台UEFI系统中的一个特殊的模块, 它将为不具备UEFI引导能力的操作系统以及16位的传统的Option ROM (即非EFI的Option ROM)提供类似于传统BIOS的系统服务. **Secure Boot**功能要求原生UEFI（即关闭或没有CSM的UEFI），因此在UEFI韧体设定中开启CSM前，需要在UEFI韧体设定中关闭Secure Boot
- **EFI应用程式**
- **GUID磁盘分区表**
在UEFI规范中, 一种突破传统MBR磁盘分区结构限制的GUID磁盘分区系统(GPT)被引入, 新结构中, 磁盘分区的主分区数不再受限制(MBR只能存在4个主分区)
UEFI+*GUID磁碟分割表*(GUID Partition Table, 缩写GPT)结合可以支持2.1TB以上的磁盘

## Secure Boot
> 只允许载入有适当位数签章的EFI驱动程式和EFI启动程式,

> Secure Boot内置于UEFI BIOS中, 用来对抗感染MBR, BIOS的恶意软件, win8缺省将使用Secure Boot, 在启动过程中, 任何要加载的模块必须签名(强制的), UEFI固件会进行验证, 没有签名或者无法验证的, 将不会加载

# 磁盘分区
## MBR和主引导扇区的关系
> ![](https://img-blog.csdn.net/20140223134137000?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGlhb21pbnRoZXJl/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
> ![](https://img-blog.csdn.net/20140223142722843?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveGlhb21pbnRoZXJl/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
> 主引导扇区是硬盘0号柱面, 0号磁头的第一个扇区, 大小为512个字节(硬盘可以用柱面, 磁头, 扇区定位)

## 主分区
> 分区表DPT共64字节, 记录硬盘有多少分区以及分区的各种属性. 一个分区的信息要占用16字节, 所以分区表只能定义4个分区, 所以*基本硬盘*最多能分4个主分区

## 扩展分区
> 最多存在一个, 若存在则至少包含一个逻辑分区

## 逻辑分区
> 逻辑分区必须建立在扩展分区中

# 先装win后装linux好
linux的引导加载程序grub既能识别linux的核心启动文件，也能识别windows的核心启动文件。而windows的引导加载程序却不能识别linux的核心启动文件，如果先装linux的，后装windows的话，由于windows默认把引导加载程序安装在MBR与超级块中，这样的话就覆盖掉原来的linux的grub了，导致磁盘的MBR只能识别windows的而不能进入linux了，所以每次加载BIOS信息后，你只能毫无选择的进入windows了

# 磁盘
## 基本磁盘
> 基本磁盘受26个字母限制, 盘符只能是26个英文字母中的一个. 其中A, B已经被软驱占用, 实际可用盘符只要24个.

## 动态磁盘
> 不受分区数量限制, 可以创建的盘集个数没有限制
优点:
- 可以将磁盘容量扩展到非邻近的磁盘空间
- 可以在不重启机器的情况下调整动态磁盘大小而不会丢失损坏已有的数据

# 分区表
## MBR分区表
> 主引导记录（Master Boot Record，缩写：MBR），又叫做主引导扇区，是计算机开机后访问硬盘时所必须要读取的首个扇区，它在硬盘上的三维地址为（柱面，磁头，扇区）＝（0，0，1）
- 在MBR硬盘中，分区信息直接存储于主引导记录（MBR）中（主引导记录中还存储着系统的引导程序）

## GPT分区表
![GUID Partition Table Scheme](https://upload.wikimedia.org/wikipedia/commons/thumb/0/07/GUID_Partition_Table_Scheme.svg/600px-GUID_Partition_Table_Scheme.svg.png)
GPT分区表的结构. 在上例中, 每个逻辑块(LBA)为512字节, 每个分区的记录为128字节. 负数的LBA地址表示从最后的块开始倒数, -1表示最后一个块

### 特点, 不同
- 在GPT硬盘中，分区表的位置信息储存在GPT头中。但出于兼容性考虑，硬盘的第一个扇区仍然用作MBR，之后才是GPT头
- 跟现代的MBR一样，GPT也使用逻辑区块位址（LBA）取代了早期的CHS寻址方式
- 传统MBR信息存储于LBA 0，GPT头存储于LBA 1
- 为了减少分区表损坏的风险，GPT在硬盘最后保存了一份分区表的副本

## 分区详解
### 传统MBR (LBA 0)
在GPT分区表的最开头，出于兼容性考虑仍然存储了一份传统的MBR，用来防止不支持GPT的硬盘管理工具错误识别并破坏硬盘中的数据，这个MBR也叫做*Protective MBR*

### 分区表头 (LBA 1)
- 分区表头定义了硬盘的可用空间以及组成分区表的项的大小和数量
- 分区表头还记录了这块硬盘的GUID(Globally Unique Identifier全局唯一标识符), 记录了分区表头本身的位置和大小（位置总是在LBA 1）以及备份分区表头和分区表的位置和大小（在硬盘的最后）

### 分区表项（LBA 2–33）


## ESP分区表
> EFI system partition, 该分区用于采用了EFI BIOS的电脑系统，用来启动操作系统。分区内存放引导管理程序、驱动程序、系统维护工具等。如果电脑采用了EFI系统，或当前磁盘用于在EFI平台上启动操作系统，则应建议ESP分区。



reference list:

- [如何在 Linux 下安装 Windows 7？ - 薛莲晓](https://www.zhihu.com/question/23039001/answer/139007302)
- [BIOS](https://zh.wikipedia.org/wiki/BIOS)
- [统一可延展韧体介面](https://zh.wikipedia.org/wiki/%E7%B5%B1%E4%B8%80%E5%8F%AF%E5%BB%B6%E4%BC%B8%E9%9F%8C%E9%AB%94%E4%BB%8B%E9%9D%A2)
- [MBR, 多种分区定义](http://blog.51cto.com/matthewfjnd/2294325)
- [基本磁盘, 动态磁盘, MBR磁盘, GPT磁盘](http://blog.51cto.com/a36900/374595)
- [GPT MBR 分区](https://www.cnblogs.com/bluestorm/p/5925924.html)
- [全局唯一标识分区表](https://zh.wikipedia.org/wiki/GUID%E7%A3%81%E7%A2%9F%E5%88%86%E5%89%B2%E8%A1%A8)
