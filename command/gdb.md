- 执行完当前循环:`u (until) 行号`

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

## 查看调用栈

backtrace 或 bt

## 其他操作

上一个命令: `Ctrl-p`

下一个命令: `Ctrl-n`

执行 shell 命令: `shell 其他命令`

在 main 函数打断点并执行到 main:`start`

打印 x 的数据类型: `ptype x`

## stack

push的深度会随着数据类型的变化而变化

## 跟踪 fork 的进程

```
set follow-fork-mode parent
set follow-fork-mode child
show follow-fork-mode
```

## 跟踪 exec 之后的进程

```
catch exec
```

## 查看 pid

```
info inferior
```

## 查看 debug 的进程的文件描述符表

```
info proc(获取进程号)
shell ls -l /proc/进程号/fd
```

## 查看进程信息

```
info proc map
```

## gdbserver

```
远程
gdbserver ip:port  appname(进程名)
本地
先gdb,
然后 target remote [ip]:[port]
target remote 是关键字 不是可替代参数
```

## gdb 源码相关

设定源码搜索位置

```
directory [位置]
```

查看源码搜索位置

```
show directories
show substitute-path 
info sources
```

## 实模式下查看当前执行指令
```
(gdb) x ($cs*0x10+(int)(*$eip))
```

## 无法用 clion 默认设置远程调试 6.828 的原因:

**背景**: 远程代码已编译生成有调试符号的二进制文件,且本地与远程代码已同步,且 clion 中已经建立好 mapping 关系. 
   
**问题**: 打断点,单击 debug 按钮后不停下,直接执行到底,提示"no source file named..."

**原因**: 

首先要了解gdb 寻找源码的步骤.

1. 在编译后,二进制文件会包含一个`source path`的信息(可以通过`show directories`查看),gdb 首先在此目录下查看.如果没有找到则继续.
2. 二进制文件可能会包含"编译时目录",即它被编译时所在的目录,是一个绝对路径,如`/root/foo`. gdb首先查看当前的 gdb session 是否设置了`substitute-path`,如果设置了,比如设置成了`/root/ -> /root/User/bar`,那么就把编译时目录进行替换:`/root/User/bar/foo`,然后在此目录下查找.通常适用于远程调试的环境,clion 的 mapping 本质上就是按此设置.如果还没找到,则继续
3. 最后在`current working directory`寻找.可以通过`pwd`来查看此路径.


我们的问题发生的过程是, 6.828 的编译结果不含编译时目录,于是设置的 mapping 自然无法替换;于是 gdb 尝试在当前工作目录下查找,而 clion 启动的 gdb 的初始工作目录是 clion 程序所在的文件夹,自然无法找到.

二进制文件至少会记录文件名,可以用`info sources`查看.如果 mapping 成功,则会显示绝对路径.

**解决方法**

在~/.gdbinit 中用`set directory`设置`source path`即可.

在 ucore 中: 

如何操作?

2019-11-02 再次遇到这个问题,之前写的太粗糙了,在哪敲命令都没指出来.



参考链接: ftp://ftp.gnu.org/old-gnu/Manuals/gdb-4.17/html_node/gdb_49.html




参考资料:

- [参考链接](http://visualgdb.com/gdbreference/commands/x)

- [Youtube: CppCon 2016: Greg Law “GDB - A Lot More Than You Knew"](https://www.youtube.com/watch?v=-n9Fkq1e6sg)


## clion 远程调试

- clion 的 mapping 是必填字段,否则刚连上就会断开
- 而且要把二进制文件复制到本地,否则断点不会断.可以用 clion 的 remote host 直接拖过来.
- 断点无效的另一个常见原因是编译时对应代码被优化掉了.查看是否指定了 -O0 .

## 常用的 set

set print object on
set print pretty on
set print vtbl on

show print object
show print pretty
show print vtbl

set disassembly-flavor intel

## 虚函数表
p /a (*(void ***)obj)[0]@10

## 带参调试

gdb --args a.out arg1 arg2 arg3

## 输出重定向
call close(1)
call close(2)
call open("/dev/pts/1", 2)
call open("/dev/pts/1", 2)

## 调试心得

多多利用栈信息,跳转到当前或上个函数的位置

## 如何注释?

自底向上, ...是对...的封装

## 关于 gdb 的再总结

gdb 调试有三个元素: 源码, 可执行文件, 进程.

通常`gdb program`会直接执行可执行文件,创建进程, 并关联到代码. 这意味着二进制文件应该存储着源码路径信息.

二进制文件可能没有完整的源码路径,此时就需要用`directory`来指定.如果是 clion,只能在`.gdbinit`中指定.


## 进程相关

命令 | 含义
------- | -------
info inferiors | 当前调试的进程


## scheduler-locking

set scheduler-locking off|on|step


- off 不锁定任何线程,即所有线程都执行
- on 只有当前被调试程序会执行
- step 在单步的时候，除了next过一个函数的情况以外，只有当前线程会执行。

一些术语

模式名称 | 含义
-----|---
all-stop mode | 全停模式
single-stepping | 单步执行
scheduler-locking | 调度锁
schedule-multiple | 多进程调度
record mode | 记录模式
replay mode | 回放模式

## 窗口布局