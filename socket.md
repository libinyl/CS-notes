## 1 socket 

### 原型
```C
int
socket(int domain, int type, int protocol);
```

family | 说 明
-------|----
AF_INET | IPv4协议
AF_INET6 | IPv6协议
AF_LOCAL | Unix域协议（见第15章）
AF_ROUTE | 路由套接字（见第18章）
AF_KEY | 密钥套接字（见第19章）

type | 说 明
-----|----
SOCK_STREAM | 字节流套接字
SOCK_DGRAM | 数据报套接字
SOCK_SEQPACKET | 有序分组套接字
SOCK_RAW | 原始套接字

protocol 参考 <netinet/in.h>
protocol | 说 明
---------|----
IPPROTO_TCP | TCP传输协议
IPPROTO_UDP | UDP传输协议
IPPROTO_SCTP | SCTP传输协议
IPPROTO_IP | IP族通用

###  示例

```C
int sockfd;
if((sockfd = socket(AF_INET, SOCK_STREAM, IPPROTO_IP)) == -1){}
```

## 2 bind

把地址A (和/或) 端口P捆绑到套接字S.

### 原型

```C

int
bind(int socket, const struct sockaddr *address, socklen_t address_len);
```
### 示例

```C
bind(sockfd, (SA *) &servaddr, sizeof(servaddr));
```

## 端口

## 端口分类

- Well-Known Ports: [0, 1023)
- Registered Ports: [1024, 49152)
- Dynamic Ports:[49152, 65535) 通常不指定

## socket 选项

- 所有 TCP 服务器都应设置`SO_REUSEADDR`

## 常用函数

- inet_pton: 

**主机字节序 -> 网络字节序**

- htons: `unsigned short integer hostshort`
- htonl: `unsigned integer hostlong`

**text(点分十进制)->binary(二进制整数)**

- inet_pton

## 服务器启动之后,能观察到的状态有什么?

1. `/proc/pid/fd` 中新增了 socket fd.对应的 inode 可以在`cat /proc/net/tcp`下观察.

```shell
root@hw1:/proc/1857/fd# ll
total 0
dr-x------ 2 root root  0 Oct 11 15:58 ./
dr-xr-xr-x 9 root root  0 Oct 11 15:54 ../
lrwx------ 1 root root 64 Oct 11 15:59 0 -> /dev/pts/0
lrwx------ 1 root root 64 Oct 11 15:59 1 -> /dev/pts/0
lrwx------ 1 root root 64 Oct 11 15:59 2 -> /dev/pts/0
lrwx------ 1 root root 64 Oct 11 15:59 3 -> 'socket:[23853]'
```

2. netstat 增加了 LISTEN 条目.

```shell
root@hw1:/proc/net# netstat -a |grep 2222
tcp        0      0 0.0.0.0:2222            0.0.0.0:*               LISTEN
```

3. `tcp_info`的状态被置为 TCP_LISTEN.

### 用 tcpdump 监控三次握手

**环境准备**

![](/images/三次握手验证.png)

![](/images/三次握手验证&#32;2.png)

**握手完毕,开始验证**

![](/images/三次握手验证&#32;3.png)

**服务端**


root@hw1:~# tcpdump port 2222
时间戳 | 协议族 | 源宿节点 | 标志位 Flags | 序列号 | 窗口大小 Windows Size | 选项 | 数据段长度 length
----|-----|------|-----------|---------------------|-------------------|----|-------------
16:16:10.901818 | IP | ecs-119-3-221-5.compute.hwclouds-dns.com.42570 > hw1.2222: | Flags [S], | seq 1855962664, | win 29200, | options [mss 1460,sackOK,TS val 2176936535 ecr 0,nop,wscale 7], | length 0
16:16:10.901897 | IP | hw1.2222 > ecs-119-3-221-5.compute.hwclouds-dns.com.42570: | Flags [S.], | seq 1914836072, ack 1855962665, | win 28960, | options [mss 1460,sackOK,TS val 2786922665 ecr 2176936535,nop,wscale 7], | length 0
16:16:10.902314 | IP | ecs-119-3-221-5.compute.hwclouds-dns.com.42570 > hw1.2222: | Flags [.], | ack 1, | win 229, | options [nop,nop,TS val 2176936536 ecr 2786922665], | length 0



**客户端**

root@hwtime:~# tcpdump port 2222
时间戳 | 协议族 | 源宿节点 | 标志位 Flags | 序列号 | 窗口大小 Windows Size | 选项 | 数据段长度 length
----|-----|------|-----------|---------------------|-------------------|----|-------------
16:16:10.901491 | IP | hwtime.42570 > ecs-117-78-3-185.compute.hwclouds-dns.com.2222: | Flags [S], | seq 1855962664, | win 29200, | options [mss 1460,sackOK,TS val 2176936535 ecr 0,nop,wscale 7], | length 0
16:16:10.902150 | IP | ecs-117-78-3-185.compute.hwclouds-dns.com.2222 > hwtime.42570: | Flags [S.], | seq 1914836072, ack 1855962665, | win 28960, | options [mss 1460,sackOK,TS val 2786922665 ecr 2176936535,nop,wscale 7], | length 0
16:16:10.902161 | IP | hwtime.42570 > ecs-117-78-3-185.compute.hwclouds-dns.com.2222: | Flags [.], | ack 1, | win 229, | options [nop,nop,TS val 2176936536 ecr 2786922665], | length 0

注:

- `[S]`:  SYN
- `[S.]`: SYN, ACK
- `[.]`: ACK


将以上输出简化且按时序合并:

**服务端(S)简化**

时间戳 | 协议族 | 源宿节点 | 标志位 Flags | 序列号 | 窗口大小 Windows Size | 选项 | 数据段长度 length
----|-----|------|-----------|---------------------|-------------------|----|-------------
16:16:10.901818 | IP | C > S: | Flags [S], | seq 1855962664, | win 29200, | options [mss 1460,sackOK,TS val 2176936535 ecr 0,nop,wscale 7], | length 0
16:16:10.901897 | IP | S > C: | Flags [S.], | seq 1914836072, ack 1855962665, | win 28960, | options [mss 1460,sackOK,TS val 2786922665 ecr 2176936535,nop,wscale 7], | length 0
16:16:10.902314 | IP | C > S: | Flags [.], | ack 1, | win 229, | options [nop,nop,TS val 2176936536 ecr 2786922665], | length 0


**客户端(C)简化**

root@hwtime:~# tcpdump port 2222
时间戳 | 协议族 | 源宿节点 | 标志位 Flags | 序列号 | 窗口大小 Windows Size | 选项 | 数据段长度 length
----|-----|------|-----------|---------------------|-------------------|----|-------------
16:16:10.901491 | IP | C > S: | Flags [S], | seq 1855962664, | win 29200, | options [mss 1460,sackOK,TS val 2176936535 ecr 0,nop,wscale 7], | length 0
16:16:10.902150 | IP | S > C: | Flags [S.], | seq 1914836072, ack 1855962665, | win 28960, | options [mss 1460,sackOK,TS val 2786922665 ecr 2176936535,nop,wscale 7], | length 0
16:16:10.902161 | IP | C > S: | Flags [.], | ack 1, | win 229, | options [nop,nop,TS val 2176936536 ecr 2786922665], | length 0

实际上分析客户端或服务端,道理是一样的.它们除了时间其他的都一样(?).

**选项解释**

MSS:  最大段大小

**字段解释**

序列号:

响应号:

**标志位解释**

- SYN: 是否初始序列号
- ACK: 在数据传输阶段,指明已经收到的最大字节(+1).
- RST: 重置链接

### tcp 序列号 SEQ 的格式是怎样的?

### tcp 之下的协议(IP)会产生哪些需要修复的问题?

- 重复
- 丢包
- 错误

## 数据类型

ip地址: struct sockaddr