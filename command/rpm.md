## rpm

参考: https://www.cnblogs.com/gmlkl/p/9354254.html#_label6

查看 rpm 包内容: rpm -qpl packetname.rpm

## 安装

rpm -i 需要安装的包文件

rpm -iv 需要安装的包文件(显示安装详情)

rpm -ivh 需要安装的包文件(显示安装详情及进度)

加上 --force 属性，强制进行安

## 查询系统已经安装的软件
rpm -qa

## 卸载

rpm -e xxx