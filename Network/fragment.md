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
简单地说，高层可以隔离低层的域。

<br/><br/>reference list:
- [帧, 数据包, 数据报](https://blog.csdn.net/qq_25606103/article/details/51295965)
- [1][网络扫盲—什么是核心层/汇聚层/接入层](https://loris-jand.iteye.com/blog/1989181)
