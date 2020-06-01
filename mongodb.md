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

