

执行完当前循环:

```
u (until)
```
## 断点

查看当前所有断点
```
info b
i b
```
删除断点:
```
d 断点号
d 断点号范围 如 1-10
```

在某文件某行打断点

```
b 文件名:函数名
```
在某文件某行打断点:
```
b 文件名:行号
```
查看某断点的代码
```
info b
```
## 栈信息
```
f
```

查看当前栈局部变量/参数

```
info locals
info args
```

## 内存信息(在线[文档](http://visualgdb.com/gdbreference/commands/x))

以指令格式查看从地址 0xf010ff46 开始的内存的20个值(注:20 个值向内存增长方向排布,与小端系统相反,需要注意):

```
x/20i 0xf010ff46
```

直接查看内存段信息:
```
x/10x $sp
```

其中把 i 可以更换,以其他格式查看数据.

## 界面布局

切换视图多布局样式:`Ctrl-x 2`

切换是否多视图:`Ctrl-x a`

## 其他操作

上一个命令: `Ctrl-p`

下一个命令: `Ctrl-n`

执行 shell 命令: `shell 其他命令`

在 main 函数打断点并执行到 main:`start`

打印 x 的数据类型: `ptype x`

## stack

push的深度会随着数据类型的变化而变化



参考资料:

- [参考链接](http://visualgdb.com/gdbreference/commands/x)

- [Youtube: CppCon 2016: Greg Law “GDB - A Lot More Than You Knew"](https://www.youtube.com/watch?v=-n9Fkq1e6sg)