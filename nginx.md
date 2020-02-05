## nginx 与 php 的配置

外部请求=>nginx => php-fpm => php 

nginx 可以通过配置 把 php 请求 转发给 php-fpm处理. 

php-fpm 需要配置监听,在php-fpm.conf中配置.

### 配置 php-fpm

php-fpm.conf 位于 /usr/local/php5/etc

修改 listen 为 listen = /usr/local/nginx/logs/php-cgi.sock

## 配置 nginx.conf

nginx.conf 位于 /usr/local/nginx/conf

location 中加入

       location ~ .*\.(php|php5)?$
        {
        	#fastcgi_pass  127.0.0.1:9000;
         	fastcgi_pass  unix:/usr/local/nginx/logs/php-cgi.sock;
         	fastcgi_index index.php;
         	include fastcgi.conf ;
        }

## 启动 php-fpm



## nginx

缓存立刻生效

killall php-fpm

./php-fpm -c /usr/local/php7/etc/php.ini -y /usr/local/php7/etc/php-fpm.conf

## nginx 与 php

https://blog.csdn.net/aloha12/article/details/88852714

nginx 监听外部请求,可以通过配置, 把 php 请求 转发给 php-fpm处理. 

php-fpm 需要配置监听,在php-fpm.conf中配置.

## php-fpm.conf

位于 /usr/local/php5/etc


请求会被location ~ \.php${ ... }catch住，也就是进入 FastCGI 的处理程序（nginx需要通过FastCGI模块配置，将相关php参数传递给php-fpm处理。在该项中设置了fastcgi_pass相关参数，将用户请求的资源发给php-fpm进行解析，这里涉及到nginx FastCGI模块的相关配置语法下文会介绍）


Nginx配置.之PHP FastCGI

Nginx和PHP-FPM的进程间通信有两种方式,一种是TCP,一种是UNIX Domain Socket.
其中TCP是IP加端口,可以跨服务器.而UNIX Domain Socket不经过网络,只能用于Nginx跟PHP-FPM都在同一服务器的场景.用哪种取决于你的PHP-FPM配置:
方式1:
php-fpm.conf: listen = 127.0.0.1:9000
nginx.conf: fastcgi_pass 127.0.0.1:9000;
方式2:
php-fpm.conf: listen = /tmp/php-fpm.sock
nginx.conf: fastcgi_pass unix:/tmp/php-fpm.sock;
其中php-fpm.sock是一个文件,由php-fpm生成,类型是srw-rw----.

UNIX Domain Socket可用于两个没有亲缘关系的进程,是目前广泛使用的IPC机制,比如X Window服务器和GUI程序之间就是通过UNIX Domain Socket通讯的.这种通信方式是发生在系统内核里而不会在网络里传播.UNIX Domain Socket和长连接都能避免频繁创建TCP短连接而导致TIME_WAIT连接过多的问题.对于进程间通讯的两个程序,UNIX Domain Socket的流程不会走到TCP那层,直接以文件形式,以stream socket通讯.如果是TCP Socket,则需要走到IP层,对于非同一台服务器上,TCP Socket走的就更多了.

UNIX Domain Socket:
Nginx <=> socket <=> PHP-FPM
TCP Socket(本地回环):
Nginx <=> socket <=> TCP/IP <=> socket <=> PHP-FPM
TCP Socket(Nginx和PHP-FPM位于不同服务器):
Nginx <=> socket <=> TCP/IP <=> 物理层 <=> 路由器 <=> 物理层 <=> TCP/IP <=> socket <=> PHP-FPM

像mysql命令行客户端连接mysqld服务也类似有这两种方式:
使用Unix Socket连接(默认):
mysql -uroot -p --protocol=socket --socket=/tmp/mysql.sock
使用TCP连接:
mysql -uroot -p --protocol=tcp --host=127.0.0.1 --port=3306

## 配置文件自动还原问题

## 配置目录

/usr/local/nginx/conf

