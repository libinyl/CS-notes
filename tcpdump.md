## tcpdump 常用命令

- -i <eth0> 指定网络接口(interface)
- -n 不把主机的网络地址转换成名字
- -S 打印绝对序列号而非相对序列号
- 'port 2222' 监控指定端口
- -A

## 抓取 localhost:

sudo tcpdump -i lo port 1234

## 只过滤 ip

 sudo tcpdump  ip host [ip]

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

                     TCPDUMP FLAGS
Unskilled =  URG  =  (Not Displayed in Flag Field, Displayed elsewhere) 
Attackers =  ACK  =  (Not Displayed in Flag Field, Displayed elsewhere)
Pester    =  PSH  =  [P] (Push Data)
Real      =  RST  =  [R] (Reset Connection)
Security  =  SYN  =  [S] (Start Connection)
Folks     =  FIN  =  [F] (Finish Connection)
          SYN-ACK =  [S.] (SynAcK Packet)
                     [.] (No Flag Set)

## http 抓包

tcpdump tcp port 80 -n -X -s 0

tcpdump -i eth1 host api.rainbow.oa.com -nv


## 抓取 http

# tcpdump filter for HTTP GET 
sudo tcpdump -s 0 -A 'tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x47455420'

# tcpdump filter for HTTP POST 
sudo tcpdump -s 0 -A 'tcp dst port 80 and (tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x504f5354)'

 tcpdump -i <网卡名称> tcp and port <端口号> -n -nn -v -vv -w cache -W 100:100个文件 -C 30:文件大小30M -s 80：只抓包前面的80字节  -Z <用户名称如root>
