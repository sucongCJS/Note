# 名词
- PDU: protocol data unit协议数据单元

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


<br/><br/>reference list:
- [帧, 数据包, 数据报](https://blog.csdn.net/qq_25606103/article/details/51295965)
