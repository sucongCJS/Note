- PDU: protocol data unit协议数据单元
# 名词

## Internet Access Tech
## Four Basic Characteristics
- Fault Tolerance: 多条线路, multipleconnection,
- Scalability: the ability to expand or reduce devices
- Quanlity of Service (QoS):
  - Security:

## Extranet

## Network Interface Card

## MAC Address
> Media Access Contril Address

48 位

### MAC frame structure:
1. Receiver MAC address
2. Sender MAC address
.
. framce check sequence
.

Frame Header, Frame Trailer

# topology
## ring topology
the host who has token can speak
## mesh topology

# broadcast
## unicast
> A Unicast transmission/stream sends IP packets to a single recipient on a network.

If the streaming video is to be distributed to a single destination, then you would start a Unicast stream by setting the destination IP address and port on the AVN equal to the destination’s values.

## multicast
> A Multicast transmission sends IP packets to a group of hosts on a network

If you want to view the stream at multiple concurrent locations, then you would set the AVN’s destination IP address to a valid Multicast IP address (224.0.0.0 – 239.255.255.255)


# points
二层的PDU叫做Frame;
IP Packets are also reffered to as IP datagrams by many;

## 广播地址
> broadcast

host_ID全为1的IP地址为广播地址. 例如对于 10.1.1.0/24 网段, 其广播地址为 10.1.1.255, 即当发送的一个目的地址为 10.1.1.255的分组(封包)时, 它将被发送给该网段上的所有主机
受限的广播地址是 255.255.255.255. 该地址用于主机配置过程中...


# 同个网段内的通信(A->B)
frame没有被填完不能发送
- A有A.MAC, A.IP, B.IP, 没有B.MAC
- Arp request来获得B.MAC
  -

要在同一个网段因为要有同一个广播地址
packet never changes, only the frame challenges

# 不同网段内的通信(A->D)
- 没有D的MAC, 用route的MAC
-

# 层次化网络设计[1]
- 核心层(core layer)
  - keywords: back bone, optimized, reliable, high speeds
  - 为网络提供骨干组件或高速交换组件，高效速度传输是核心层的目标
  - 拥有更高的可靠性，性能和吞吐量
- 汇聚层(distribution layer)
  - it defines policy for the network which is used to handle certain kinds of traffic including Routing updates, Route summaries, VLAN traffic and Address aggregation(地址聚合)
  - 是核心层和终端用户接入层的分界面，汇聚层完成网络访问的策略控制、广播域的定义、VLAN间的路由、数据包处理、过滤寻址及其他数据处理的任务
  - 是多台接入层交换机的汇聚点，它必须能够处理来自接入层设备的所有通信量，并提供到核心层的上行链路，因此汇聚层交换机与接入层交换机比较，需要更高的性能，更少的接口和更高的交换速率
- 接入层(access layer)
  - 向本地网段提供用户接入、主要提供网络分段、广播能力、多播能力、介质访问的安全性、MAC地址的过滤和路由发现等任务
  - 目的是允许终端用户连接到网络，因此接入层交换机具有低成本和高端口密度特性

## 三层交换机
![三层交换机](../resource/三层交换机.png)
[计算机网络补充知识：VLAN间通信的实现方法—使用三层交换机](https://www.bilibili.com/video/av51511189)


## 冲突域广播域[link](https://feichashao.com/broadcast_domain_calculation/)
### 冲突域
> 在使用CSMA/CD传统以太网的年代，一台主机发出的比特，同一条网线相连的其他主机也能接收到这个比特。也就是说，如果其中一主机发出比特，其他主机再发出比特，那就会产生冲突了。
【分层】冲突域属于OSI第一层(物理相连的主机间会冲突);

### 广播域
> 广播域是一个区域(或者说集合)，在这个区域内，任一设备发出广播帧，其他设备都能接收到这个广播帧。
【分层】广播域属于OSI第二层(数据链路层);

### 隔离规则
三层设备能隔离二层域和一层域：路由器可以隔离广播域和冲突域
二层设备能隔离一层域：交换机可以隔离冲突域；
简单地说，高层可以隔离低层的域

# IPv6
[IPv6地址格式及子网划分方法](https://blog.csdn.net/qq_20240999/article/details/60364484)
- 地址长度128bit
- 十六进制数表示法表示的IPv6地址中, 如果几个连续的段值都是0, 那么这些0可以简记为::, 每个地址中只能有一个::

## 地址类型
- 单播地址(Unicast IPv6 Address)
可聚合的全球单播地址（Aggregatable Global Unicast Addresses）
可在全球范围内路由和到达的，相当于IPv4里面的global addresses。前三个bit是001
例如：2000::1:2345:6789:abcd

- 链路本地地址(Link-Local Addresses)
用于同一个链路上的相邻节点之间通信，相当于IPv4里面的169.254.0.0/16地址。IPv6的路由器不会转发链路本地地址的数据包。前10个bit是1111 1110 10，由于最后是64bit的interface ID，所以它的前缀总是fe80::/64
例如：fe80::1

- 站点本地地址(Site-Local Addresses)
对于无法访问internet的本地网络，可以使用站点本地地址，这个相当于IPv4里面的private address（10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16）。它的前10个bit是1111 1110 11，它最后是16bit的Subnet ID和64bit的interface ID，所以它的前缀是FEC0::/48

- 唯一的本地IPv6单播地址(ULA，Unique Local IPv6
  Unicast Address)
在RFC4193中标准化了一种用来在本地通信中取代单播站点本地地址的地址。ULA拥有固定前缀FD00::/8，后面跟一个被称为全局ID的40bit随机标识符

- 未指定地址(Unspecified address)
0:0:0:0:0:0:0:0 或者::
当一个有效地址还不能确定，一般用未指定地址作为源地址。未指定地址不能作为一个目标地址来使用

- 回环地址(Loopback address)
回环地址::1用于标识一个回环接口，可以使一个节点可以给自己发送数据包。相当于IPv4的回环地址127.0.0.1



<br/><br/>reference list:
- [帧, 数据包, 数据报](https://blog.csdn.net/qq_25606103/article/details/51295965)
- [1][网络扫盲—什么是核心层/汇聚层/接入层](https://loris-jand.iteye.com/blog/1989181)
