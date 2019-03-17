# 装系统
`sudo dd if=系统.img of=/dev/SD卡 bs=2M`

# ssh连
## 只有网线
1. 网线与电脑相连
2. `nm-connection-editor`
在IPV4设置中设置Method为共享其他计算机, 让树莓派和电脑连在一个网络下
3. 看有线网所在的网段, 例如为10.42.0.0/24
4. `sudo nmap -sN 10.42.0.0.24`来获得树莓派的ip
5. `ssh 树莓派ip`

# 换源
[换源](https://blog.csdn.net/hu5566798/article/details/81055002)

# [联网](https://www.embbnux.com/2016/04/10/raspberry_pi_3_wifi_and_bluetooth_setting_on_console/)

<br/><br/>reference list:
- [Ubuntu16.04 通过网线直接连接树莓派](https://blog.csdn.net/a610786189/article/details/78701860)
