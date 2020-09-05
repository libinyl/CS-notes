## mongodb

brew services start mongodb-community@4.2

ps aux | grep -v grep | grep mongod


## 安装

wget https://repo.mongodb.org/yum/redhat/7/mongodb-org/4.2/x86_64/RPMS/mongodb-org-tools-4.2.7-1.el7.x86_64.rpm
wget https://repo.mongodb.org/yum/redhat/7/mongodb-org/4.2/x86_64/RPMS/mongodb-org-shell-4.2.7-1.el7.x86_64.rpm
wget https://repo.mongodb.org/yum/redhat/7/mongodb-org/4.2/x86_64/RPMS/mongodb-org-server-4.2.7-1.el7.x86_64.rpm
wget https://repo.mongodb.org/yum/redhat/7/mongodb-org/4.2/x86_64/RPMS/mongodb-org-mongos-4.2.7-1.el7.x86_64.rpm
wget https://repo.mongodb.org/yum/redhat/7/mongodb-org/4.2/x86_64/RPMS/mongodb-org-4.2.7-1.el7.x86_64.rpm


rpm -ivh mongodb-org-tools-4.2.7-1.el7.x86_64.rpm
rpm -ivh mongodb-org-shell-4.2.7-1.el7.x86_64.rpm
rpm -ivh mongodb-org-server-4.2.7-1.el7.x86_64.rpm
rpm -ivh mongodb-org-mongos-4.2.7-1.el7.x86_64.rpm
rpm -ivh mongodb-org-4.2.7-1.el7.x86_64.rpm


 /etc/mongod.conf

 systemctl start mongod


 Job for mongod.service failed because the control process exited with error code. See "systemctl status mongod.service" and "journalctl -xe" for details.


 systemctl status mongod.service

## dump


## 基本命令

macos 开启
brew services start mongodb-community@4.2
终止
brew services stop mongodb-community@4.2


- 连接   mongo mongodb://user:password@ip:port,ip:port,ip:port

show dbs;

use test;

查看当前用户

查看有哪些集合

- show collections

- db.getCollectionNames()

auth error: sasl conversation error: unable to authenticate using mechanism "SCRAM-SHA-1": (AuthenticationFailed) Authentication failed.

加上 --authenticationDatabase admin


## 备份与导入

mongodump -h dbhost:port -d dbname -o dbdirectory -u user -p pwd --authenticationDatabase admin

mongorestore -h 127.0.0.1:27017 -d 目标表 待导入文件路径 

端口 27017

## 删除库

use a
db.dropDatabase()

给每个条目增加一个字段

db.c.update({},{$set:{'新字段名':'值'}},{multi:true})

## 聚合

db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : 1}}}])