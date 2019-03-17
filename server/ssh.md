# 远程连接服务器
除非必要, server类型的主机不建议开放远程连接服务
可以针对特定的网络开放远程连接服务, 去他来源的IP一律阻挡

## 登录类型
文字接口明文传输: Telnet(可能会被tcpdump之类的监听软件获取到数据)
文字接口加密: SSH
图形接口: XDMCP, VNC, XRDP

建议将图形接口的远程登录服务器仅开放在LAN中

# SSH服务器
> Secure SHell Protocol

默认状态下, SSH协议提供两个服务器功能:
- Shell
- Sftp-Server, 类似FTP服务, 但更安全

## 连接加密技术
### 非对称密钥系统
公钥
> 提供给远程主机进行数据加密的行为. 大家都能得到你的公钥来将数据加密
私钥
> 远程主机使用公钥加密的数据, 在本地端公私钥来解密. 私钥不能外流

公钥加密私钥解, 私钥加密公钥解

#### SSH服务器端与客户端的连接步骤:
1. Server第一次启动SSHD(BTW: the client is ssh, the daemon is sshd)时, 自动运算产生公钥(因为第一次所以没有), 存储于`/etc/ssh/ssh_host_*`
2. Client请求连接
3. Server发送公钥(明码)给Client
4. Client将公钥数据记录与`~/.ssh/known_hosts`, 并开始利用公钥加密数据
5. 发送利用公钥加密的数据





<br/><br/>reference list:
- [鸟哥的Linux私房菜-服务器架设篇]()
