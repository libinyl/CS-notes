## 显示文件夹结构:
```shell
while true;do tree;sleep 1;clear;done
```
等价于
```
watch -n 1 tree
```


## 清空文件
```
> hello.txt
```

## 基础

变量取值: ${i}

反引号内执行的是命令

## 前台与后台

把当前进程放到后台运行: `ctrl z`

查看后台任务: `jobs`

与最近的后台任务切换: `fg`

杀死后台进程: kill %[后台job号]

## 调试

sh -x file.sh   #进行脚本调试(debug)
+号行:  shell脚本实际执行的命令
++ 号行: 执行trap机制中指定的命令


## 环境变量加载顺序

![bash脚本加载顺序](/images/bash启动顺序.png)

## 判断

-eq           //等于

-ne           //不等于

-gt            //大于 （greater ）

-lt            //小于  （less）

-ge            //大于等于

-le            //小于等于



## 特殊符号

$0 | 当前脚本的文件名。
---|-------
$n（n≥1） | 传递给脚本或函数的参数。n 是一个数字，表示第几个参数。例如，第一个参数是 $1，第二个参数是 $2。
$# | 传递给脚本或函数的参数个数。
$* | 传递给脚本或函数的所有参数。
$@ | 传递给脚本或函数的所有参数。当被双引号" "包含时，$@ 与 $* 稍有不同，我们将在《Shell $*和$@的区别》一节中详细讲解。
$? | 上个命令的退出状态，或函数的返回值，我们将在《Shell $?》一节中详细讲解。
$$ | 当前 Shell 进程 ID。对于 Shell 脚本，就是这些脚本所在的进程 ID。


=~ 是否能用之后的正则匹配到


## set

set -x 追踪代码执行

## 例子

## 内置

dirname 当前目录

## 查看某程序是否启动

ps aux | grep nginx | grep -v -q grep

if [$? -ne 0] 则已启动


获取本地 ip


local_ip=`LC_ALL=C ifconfig  | grep 'inet addr:'| grep -v '127.0.0.1' | cut -d: -f2 | awk '{ print $1}'`

## 重定向权限不足

sudo sh -c 'echo abc > test.asc'

统计文件数量

ls -l|grep "^-"| wc -l

