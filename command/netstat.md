## netstat 分析

### 1 显示内容

- 网络连接
- 路由表
- 接口统计数据
- 无效连接
- 多播成员

默认是显示打开的 socket 列表.如果不指定地址族,那么所有的配置过的地址族的活动的端口都会显示.

### 2 常用选项


-a 显示所有选项.如果不指定,则不显示 LISTEN.
-l 只列出 listen
-t (tcp)仅显示tcp相关选项
- -n 拒绝显示别名，能显示数字的全部转化成数字。
- -p 显示建立相关链接的程序名

```C
netstat -atnp
```