## tcpdump 常用命令

- -i <eth0> 指定网络接口(interface)
- -n 不把主机的网络地址转换成名字
- -S 打印绝对序列号而非相对序列号
- 'port 2222' 监控指定端口

## 抓取 localhost:

sudo tcpdump -i lo port 1234

## 一些标记的全称
标志 | 含义
---|---
S | (SYN)
F | (FIN)
P | (PUSH)
R | (RST), | 
U | (URG), | 
W | (ECN CWR), 
E | (ECN-Echo)
. | (ACK)
none | (no)

## http 抓包

tcpdump tcp port 80 -n -X -s 0
