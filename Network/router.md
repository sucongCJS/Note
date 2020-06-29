- 数据包（packet）：IP 协议传送数据的单位；
- 帧（frame）：链路层传送数据的单位；
- 节点（node）：实现了 IP 协议的设备；
- 路由器（router）：可以转发不是发给自己的 IP 包的设备；
主机（host）：不是路由器的节点；
- 链路（link）：一种通信机制或介质，节点可以通过它在链路层通信。比如以太网、PPP 链接，也包括隧道；
- 接口（interface）：节点与链路的连接（可以理解为抽象的“网卡”）；
- 链路层地址（link-layer address）：接口的链路层标识符（如以太网的 mac 地址）；


# 一些口
## WAN(Wide Area Network)口
> WAN口就是路由器的外网接口, 相当于外面的进线接口, 它有自己的IP, MAC地址, 和获取IP的多种方式
> a WAN consists of multiple LANs that have been connected together over long distances using routers.

### WAN口接口类型
- PPPOE拨号
IP地址是随机分配的, 没有固定的IP地址(当这台电脑需要被外界直接访问的时候, 就需要固定的IP地址)
- 自动获取IP
一般当路由器后面还需要接路由器时, 使用自动获取IP
- L2TP
- ...

## LAN(Local Area Network)口
> LAN is a small network, this type of network is often called an *intranet*
> 
> 

LAN口就是路由器的内网接口, 它的LAN口就是它在内网之间的PC访问时的一个身份. 因此, 我们在登录路由器的时候都是通过输入路由器的LAN口, 如果路由器的LAN修改了, 那么我们输入路由器的IP也要改成修改后的IP. 修改LAN的IP一般在**多个路由器串联**时使用, 此时的路由器WAN口接口类型为自动获取
不过一般为了安全考虑，很多都是修改了LAN口IP的，比如政府机构，他们的内网IP你们一般不会知道
see more in *network.md*

## 路由器的_MAC地址_(Media Access Control Address)
> 如果说路由器的WAN口和LAN口IP地址为艺名的话，那么WAN口和LAN口的MAC地址为它的真实姓名. IP地址都是虚拟出来的地址, 好使用和识别些. MAC地址就是**物理地址**的意思.

> 比如, 有些固网服务商绑定了账号, 那就是通过账号绑定它的WAN口MAC地址, 只要换路由器的话就需要松绑, 否则是连不上的. 如果是通过电脑拨号上网的话, 然后安装路由器, 此时服务商又绑定了账号, 我们可以通过打电话叫他们松绑, 也可以通过克隆PCMAC地址来解决.

## 关于WAN口MAC、LAN口MAC、网卡MAC之间的关系
> 路由器的每个端口都会有一个自己的MAC.
> LAN的MAC就是路由器上连接电脑的一端的端口物理地址
> WAN的MAC就是路由器上连接猫或外网网线的端口物理地址
> 在自己电脑上查到的MAC地址是自己电脑网卡的MAC地址，也就是自己电脑上网口的MAC地址

## ISP(Internet Service Provider)
> an ISP is a company that owns a WAN

## IXP(Internet Exchange Points)
>

# 拨号上网
## 模拟线电话拨号
> 调制解调器(modem)将电脑的数字信号和电话线上传输的模拟信号相互转换

## 连不上网的可能原因
- 电脑IP地址和路由IP地址不在同一网段
- 如果LAN口的MAC地址被绑定了, 换路由器就需要克隆MAC地址
  - 查看MAC地址, 用`arp`
- 路由器的LAN口IP与其分配给接入设备的IP不能与WAN口IP在同一网段，不然怎么叫路由。在接入设备不能上网的情况下，检查下接入路由器的设备是不是已经能连接到路由器外的网络，比如用PING命令检查能不能PING通上外网的网关，就是刚才设置的你接入的路由器WAN口上填的网关地址，有的可能出于安全考虑不让PING，就PING一下那个绑定WAN口所在局域网中的其它电脑，看看通不能，以确定不能上网是外网上不去还是连接入的内网也上不了，以缩小故障范围

# 其他的东西
## 网关(gateway)
网关又称为下一条服务器. 在发送IP数据包时，网关定义了针对特定的网络目的地址，数据包发送到的下一跳服务器。如果是本地计算机直接连接到的网络，网关通常是本地计算机对应的网络接口，但是此时接口必须和网关一致；如果是远程网络或默认路由，网关通常是本地计算机所连接到的网络上的某个服务器或路由器

网关为`0.0.0.0`, 就意味着'unspecified', 意味着'there is none' in the context of a gateway.


## routing table
命令:`route`
flags标志说明
- U Up表示此路由当前为启动状态
- H Host，表示此网关为一主机
- G Gateway，表示此网关为一路由器
- R Reinstate Route，使用动态路由重新初始化的路由
- D Dynamically,此路由是动态性地写入–》什么时候才会有动态的路由信息呢？
- M Modified，此路由是由路由守护程序或导向器动态修改


<br/><br/>reference list:
- [路由器知识：你必须要搞懂WAN口、LAN口、MAC地址
](http://www.lotpc.com/lyqzs/5149.html)
- [路由器如何克隆MAC地址](https://service.tp-link.com.cn/detail_article_2753.html)
- [关于绑定路由器WAN口IP和MAC的](http://www.stormcn.cn/post/1475.html)
- [路由器如何克隆MAC地址？](https://service.tp-link.com.cn/detail_article_2753.html)
- [为什么网关与主机可以不在同一个网段?](https://www.zhihu.com/question/54007586/answer/137515718)
