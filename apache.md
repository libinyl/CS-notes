# apache

- 

- 查看模块

apachectl -l 

- 查看工作方式

httpd -V

- cgi 工作目录:

/var/www/cgi-bin/

文档: https://www.cnblogs.com/VseYoung/p/10018317.html

- 配置文件路径

/etc/httpd/conf/httpd.conf

debug

strace -f apache2ctl start 2>&1|grep -v " ENOENT " | grep -Ee " E[A-Z]+"
