## redis

## 命令行登陆

redis-cli -h ip -p 6379 

## 服务端启动

redis-server

## 其他

配置文件redis.conf 路径:

sudo find / -type f -name 'redis.conf'

默认位置: /etc/redis/redis.conf

如果想远程连接,需要

1. 把`bind 127.0.0.1::1`注释掉.
2. 修改protected mode 修改为：protected mode no
然后重启 redis.

### 通用命令

目标 | 命令
---|---
查看所有 key | `keys *`
清空所有 key | `flushall`
停止 | /etc/init.d/redis-server stop
启动 | /etc/init.d/redis-server start
重启 | /etc/init.d/redis-server restart

## string 命令

目标 | 命令
---|---
关联 | `set`
只有键key1不存在时才关联为 v1|`set` key1 v1 `nx`
只有键存在时才关联为 v1|`set` key1 v1 `xx`
查询 | get
键关联的整数值+1 | `incr` key1
键关联的整数值+50 | `incrby` key1 50
一次关联多个 kv| mset a 10 b 20
一次查看多个 kv| mget a b


### list 操作:


目标|命令
--|--
头部新增 | `lpush` list1 a b c
头部出列 | `lpop` list1
尾部新增 | `rpush` list1 d e f
获取范围内元素,左闭右闭 | `lrange` list1 0 1
获取范围内所有元素 | `lrange` list1 0 -1(倒数第 1 个)
阻塞获取,100秒超时| blpop list1 100


## 问题

- Authentication required.

auth "password"

## homebrew

To have launchd start redis now and restart at login:
  brew services start redis
Or, if you don't want/need a background service you can just run:
  redis-server /usr/local/etc/redis.conf