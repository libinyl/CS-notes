## zookeeper

一、zkServer.sh

1、查看 zkServer.sh 帮助信息
[root@bigdata05 bin]# ./zkServer.sh help
ZooKeeper JMX enabled by default
Using config: /bigdata/zookeeper-3.4.10/bin/../conf/zoo.cfg
Usage: ./zkServer.sh {start|start-foreground|stop|restart|status|upgrade|print-cmd}

2、 启动/关闭 zk服务器
[root@bigdata05 bin]# ./zkServer.sh start
[root@bigdata05 bin]# ./zkServer.sh stop

3、查看服务器状态
[root@bigdata05 bin]# ./zkServer.sh status
ZooKeeper JMX enabled by default
Using config: /bigdata/zookeeper-3.4.10/bin/../conf/zoo.cfg
Mode: follower


二、zkCli.sh

1、查看 zkCli.sh 帮助信息
[zk: localhost:2181(CONNECTED) 0] help
ZooKeeper -server host:port cmd args
stat path [watch]
set path data [version]
ls path [watch]
delquota [-n|-b] path
ls2 path [watch]
setAcl path acl
setquota -n|-b val path
history 
redo cmdno
printwatches on|off
delete path [version]
sync path
listquota path
rmr path
get path [watch]
create [-s] [-e] path data acl
addauth scheme auth
quit 
getAcl path
close 
connect host:port


常用命令

0）连接zookeeper
[root@bigdata05 bin]# ./zkCli.sh -server localhost:2181

1）查看当前节点列表
[zk: localhost:2181(CONNECTED) 1] ls /
[zookeeper, yarn-leader-election, hadoop-ha]

2）创建节点
[zk: localhost:2181(CONNECTED) 1] ls /
[zookeeper, yarn-leader-election, hadoop-ha]
[zk: localhost:2181(CONNECTED) 2] create /test "test"
Created /test
[zk: localhost:2181(CONNECTED) 3] ls /
[zookeeper, test, yarn-leader-election, hadoop-ha]
[zk: localhost:2181(CONNECTED) 4] create /test/test "test"
Created /test/test
[zk: localhost:2181(CONNECTED) 5] ls /
[zookeeper, test, yarn-leader-election, hadoop-ha]
[zk: localhost:2181(CONNECTED) 6] ls /test
[test]

3）查看节点数据
[zk: localhost:2181(CONNECTED) 7] get /test
test
cZxid = 0x400000031
ctime = Mon Oct 16 04:05:02 CST 2017
mZxid = 0x400000031
mtime = Mon Oct 16 04:05:02 CST 2017
pZxid = 0x400000032
cversion = 1
dataVersion = 0
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 4
numChildren = 1

4）设置节点数据
[zk: localhost:2181(CONNECTED) 8] set /test "666666"
cZxid = 0x400000031
ctime = Mon Oct 16 04:05:02 CST 2017
mZxid = 0x400000033
mtime = Mon Oct 16 04:08:44 CST 2017
pZxid = 0x400000032
cversion = 1
dataVersion = 1
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 6
numChildren = 1
[zk: localhost:2181(CONNECTED) 10] get /test
666666
cZxid = 0x400000031
ctime = Mon Oct 16 04:05:02 CST 2017
mZxid = 0x400000033
mtime = Mon Oct 16 04:08:44 CST 2017
pZxid = 0x400000032
cversion = 1
dataVersion = 1
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 6
numChildren = 1

5）删除节点
[zk: localhost:2181(CONNECTED) 11] delete /test
Node not empty: /test
[zk: localhost:2181(CONNECTED) 12] ls /
[zookeeper, test, yarn-leader-election, hadoop-ha]
[zk: localhost:2181(CONNECTED) 13] delete /test/test
[zk: localhost:2181(CONNECTED) 14] ls /test
[]
[zk: localhost:2181(CONNECTED) 15] delete /test
[zk: localhost:2181(CONNECTED) 16] ls /
[zookeeper, yarn-leader-election, hadoop-ha]

参考:

https://blog.csdn.net/zhang123456456/article/details/78243658

