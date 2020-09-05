## 常用命令

remoterun.sh

#!/sbin/sh
export DEBUG=true
export GOOS=linux
go build -o xxx main.go
scp xxx root@xx:/xxx


## 查看进程当前工作目录

pwdx pid