# 创建一个tap模式的虚拟网卡tap0
sudo ip tuntap add mode tap tap0
# 开启该网卡
sudo ip link set tap0 up
# 设置该网卡的ip及掩码
sudo ip addr add 192.168.1.1/24 dev tap0

