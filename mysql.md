## mysql

mysql 登陆:

mysql -u root -h 127.0.0.1


use mysql;
select user, host from user;

查看是否已经有 user=‘root’ 的 host 变成 %

记得最后要使用命令 flush privileges 进行刷新，不然还是

service mariadb start

## 启动

https://www.jianshu.com/p/d3f7e7402449

mysql.server stop
mysql.server start
mysql.server restart

## 查看库配置

## select 语句分析

select xxx from xx + conditionsql + limitsql + others


## 查看变量

select @@sql_mode;

## join

应当在 on 中筛选右表: 因为如果在 where 中筛选右表,有可能会损失了左表数据

应当在 where 筛选左表: 如果在 on 中筛选左表, 会返回一行 null


A CA file has been bootstrapped using certificates from the system
keychain. To add additional certificates, place .pem files in
  /usr/local/etc/openssl@1.1/certs

and run
  /usr/local/opt/openssl@1.1/bin/c_rehash

openssl@1.1 is keg-only, which means it was not symlinked into /usr/local,
because openssl/libressl is provided by macOS so don't link an incompatible version.

If you need to have openssl@1.1 first in your PATH run:
  echo 'export PATH="/usr/local/opt/openssl@1.1/bin:$PATH"' >> ~/.zshrc

For compilers to find openssl@1.1 you may need to set:
  export LDFLAGS="-L/usr/local/opt/openssl@1.1/lib"
  export CPPFLAGS="-I/usr/local/opt/openssl@1.1/include"

==> mysql
We've installed your MySQL database without a root password. To secure it run:
    mysql_secure_installation

MySQL is configured to only allow connections from localhost by default

To connect run:
    mysql -uroot

To have launchd start mysql now and restart at login:
  brew services start mysql
Or, if you don't want/need a background service you can just run:
  mysql.server start