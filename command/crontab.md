## crontab

星号顺序: 

- minute 
- hour 
- day 
- month 
- dayofweek

整数间的连字号(-)表示整数列，例如1-4意思是整数1,2,3,4

指定数值由逗号分开。如：3,4,6,8表示这四个指定整数。

符号“/”指定步进设置。“/<interger>”表示步进值.如0-59/2定义每两分钟执行一次
 

定时任务位置:/etc/cron.d/

删除定时任务脚本后还需停止相应的定时进程,才能真正停止定时任务

尝试测试: ab -c 1 http://predis1.safe.bjcc.qihoo.net:8889/cloudquery.php

## 查看所有定时任务

/etc/cron.d/

查看某个用户的定时任务

crontab -l -u username

## 查看所有用户的定时任务

cat /etc/passwd | cut -f 1 -d : |xargs -I {} crontab -l -u {}

http://tldp.org/LDP/GNU-Linux-Tools-Summary/html/scheduling.html