## 环境

安装 MYSQL

sudo apt install mysql-server

## SQL tips

- join 连接的通常都是主键.

## 常用语法复习

升序(默认): order by [字段] asc

降序: order by [字段] desc

最值: select top 1 * from...

limit: 后跟行号.如 limit 5,10 即第[5,10) 行; limit 5 即[0,5)行; 注意如果 limit 后接 1 个数字,此数字是右区间. limit 10,-1 即 [10,+∞)