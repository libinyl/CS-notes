## ip 工具

ip [ OPTIONS ] OBJECT { COMMAND | help }

ip [ -force ] -batch filename

OBJECT := 

- link
- address
- addrlabel
- route
- rule
- neigh
- ntable
- tun‐nel
- tuntap
- maddress
- mroute
- mrule
- monitor
- xfrm
- netns
- l2tp
- tcp_metrics
- token
- macsec

OPTIONS := { -V[ersion] | -h[uman-readable] | -s[tatistics] | -d[etails] |
        -r[esolve] | -iec | -f[amily] { inet | inet6 | ipx | dnet | link } |
        -4 | -6 | -I | -D | -B | -0 | -l[oops] { maximum-addr-flush-attempts }
        | -o[neline] | -rc[vbuf] [size] | -t[imestamp] | -ts[hort] | -n[etns]
        name | -a[ll] | -c[olor] -br[ief] }

查看本地路由表:

ip route show table local

# 创建一个tap模式的虚拟网卡tap0
sudo ip tuntap add mode tap tap0
# 开启该网卡
sudo ip link set tap0 up
# 设置该网卡的ip及掩码
sudo ip addr add 192.168.1.1/24 dev tap0