## PS

## 概览

**三种风格**

- UNIX 选项,必须有`-`
- BSD 选项,必须没有`-`
- GNU 选项,有两个`-`

**默认无参输出**

- 当前用户在当前窗口下所有的进程

**查看进程阻塞原因**

`ps -o pid,ppid,tty,stat,args,wchan`

- -o: 以接下来的关键字为列头显示

**命令逐次解释:**

- 默认排序规则: 1)controlling terminal 2)pid

**显示线程**

ps -aL 

ps -axuw

1. USER
2. PID
3. %CPU
4. %MEM
5. VSZ
6. RSS
7. TTY
8. STAT START   
9. TIME COMMAND

## 查看启动时间