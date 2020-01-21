## php

## php.ini 在哪?

php --ini

## php文件修改后立刻生效?

如何令 php.ini生效?

## php-fpm 位置

/usr/local/php5/sbin/php-fpm

## 杀死所有 fpm

sudo kill -9 `ps aux |grep php |grep -v grep | awk '{print $2;}'`


 sudo /usr/local/php5/sbin/php-fpm 